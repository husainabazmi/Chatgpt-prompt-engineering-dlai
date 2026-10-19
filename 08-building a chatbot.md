# 08. Building a Custom Chatbot with LLMs

# Objective

Learn how to build a conversational chatbot using the OpenAI Chat Completions API, maintain conversation context across multiple turns, and convert a conversation into a structured JSON order summary.

# Key Concepts

- Chat Completions API: Takes a list of messages and generates an assistant response.
- Message roles: `system` defines behavior, `user` provides input, and `assistant` represents the model's responses.
- Conversation context: Previous messages are included so the chatbot can respond using information from earlier turns.
- System instructions: Define the chatbot's role, menu, conversation flow, and response style.
- Temperature: Controls response variability. A low value is useful for predictable tasks.
- Structured output: JSON organizes collected order details into a format that another application can process.

# Project: OrderBot — Pizza Ordering Chatbot

# Overview

OrderBot is a pizza restaurant ordering assistant built with Python, the OpenAI API, and Panel. It guides customers through the ordering conversation and generates a JSON summary of the order.

# Technologies Used

- Python
- OpenAI Python SDK
- Chat Completions API
- Panel
- JSON

# Code Implementation

# 1. Connect to OpenAI

Import the required libraries, initialize the API client, and define a helper function for generating responses.

```python
import os
import json
import panel as pn
from openai import OpenAI

client = OpenAI()  # Reads OPENAI_API_KEY from environment
MODEL = "gpt-4o-mini"


def get_completion_from_messages(messages, temperature=0):
    response = client.chat.completions.create(
        model=MODEL,
        messages=messages,
        temperature=temperature
    )
    return response.choices[0].message.content
```

The helper function accepts the conversation history and returns the assistant's response text.

# 2. Define the Chatbot Context and Menu

The system message establishes the chatbot's role, ordering workflow, available items, prices, and safety instructions.

```python
system_message = """
You are OrderBot, a friendly pizza restaurant ordering assistant.

Follow this conversation flow:
1. Greet the customer.
2. Collect the complete order.
3. Clarify pizza sizes, quantities, toppings, and extras.
4. Ask whether the order is pickup or delivery.
5. Ask for a delivery address if delivery is selected.
6. Summarize the order and ask if anything needs changing.
7. Confirm the order before finishing.
8. Ask for the preferred payment method.

MENU AND PRICES:

Pizzas:
Pepperoni pizza:
Large 12.95, Medium 10.00, Small 7.00

Cheese pizza:
Large 10.95, Medium 9.25, Small 6.50

Eggplant pizza:
Large 11.95, Medium 9.75, Small 6.75

Sides:
Fries: Large 4.50, Small 3.50
Greek salad: 7.25

Toppings:
Extra cheese 2.00
Mushrooms 1.50
Sausage 3.00
Canadian bacon 3.50
AI sauce 1.50
Peppers 1.00

Drinks:
Coke: Large 3.00, Medium 2.00, Small 1.00
Sprite: Large 3.00, Medium 2.00, Small 1.00
Bottled water: 5.00

IMPORTANT:
- Ask for a size when the item has multiple sizes.
- Clarify quantities and toppings.
- Prices are in dollars.
- Calculate the total using the menu prices.
- Be conversational, friendly, and concise.
- Ask one or two questions at a time.
- Never claim an order has been placed unless the application
  actually has an order-submission system.
- Never request card numbers, CVVs, or banking passwords.
- Collect only the customer's preferred payment method.
"""

context = [
    {"role": "system", "content": system_message}
]
```

The `context` list stores the system instructions and will grow as the conversation continues.

# 3. Create the Chat Interface

Panel provides the components used to display messages, accept customer input, and generate the order summary.

```python
pn.extension()

chat_history = pn.Column(
    sizing_mode="stretch_width",
    scroll=True,
    height=400
)

inp = pn.widgets.TextInput(
    name="Your message",
    placeholder="Type your pizza order here...",
    value="Hi"
)

chat_button = pn.widgets.Button(
    name="Send",
    button_type="primary"
)

summary_button = pn.widgets.Button(
    name="Generate Order JSON"
)

summary_output = pn.pane.Markdown(
    "Your order summary will appear here.",
    sizing_mode="stretch_width"
)
```

# 4. Handle Customer Messages

This function adds the user's message to the conversation history, sends the complete context to the model, stores the assistant's response, and displays both messages in the interface.

```python
def collect_messages(event=None):
    prompt = inp.value.strip()

    if not prompt:
        return

    # Clear the input box
    inp.value = ""

    # Display the customer's message
    chat_history.append(
        pn.Row(
            pn.pane.Markdown(
                f"**You:** {prompt}",
                width=650
            )
        )
    )

    # Add the message to conversation history
    context.append({
        "role": "user",
        "content": prompt
    })

    try:
        response = get_completion_from_messages(
            context,
            temperature=0
        )

        # Save the assistant's response for future turns
        context.append({
            "role": "assistant",
            "content": response
        })

        # Display the assistant's response
        chat_history.append(
            pn.Row(
                pn.pane.Markdown(
                    f"**OrderBot:** {response}",
                    width=650,
                    styles={
                        "background": "#F6F6F6",
                        "padding": "10px",
                        "border-radius": "8px"
                    }
                )
            )
        )

    except Exception as error:
        chat_history.append(
            pn.pane.Markdown(
                f"**Error:** {str(error)}"
            )
        )


chat_button.on_click(collect_messages)
```

How it works:

1. The function reads the customer's input.
2. The user message is appended to `context`.
3. The model receives the updated conversation history.
4. The assistant's response is appended to `context`.
5. The response is displayed in the chat interface.

Saving both sides of the conversation allows the chatbot to use earlier information when responding to later messages.

# 5. Generate a JSON Order Summary

This function asks the model to extract order details from the conversation and return them as JSON.

```python
def generate_order_summary(event=None):
    if len(context) <= 1:
        summary_output.object = (
            "Start a conversation and place an order first."
        )
        return

    summary_instructions = """
Create a JSON summary of the customer's order using the
conversation history.

Return valid JSON only, using this structure:

{
  "pizza": [
    {
      "item": "Cheese pizza",
      "size": "Medium",
      "quantity": 1,
      "unit_price": 9.25,
      "toppings": [],
      "subtotal": 9.25
    }
  ],
  "drinks": [],
  "sides": [],
  "order_type": "Pickup",
  "delivery_address": null,
  "payment_method": null,
  "total_price": 9.25,
  "currency": "USD",
  "order_status": "Pending confirmation"
}

Rules:
- Include the size, quantity, unit price, and subtotal for each item.
- Include the price and quantity of each drink, side, and topping.
- Include toppings in the appropriate pizza entry.
- Calculate the total from the menu prices and quantities.
- Do not invent items, sizes, quantities, addresses, or payment methods.
- Use null for information that has not been provided.
- If the order is incomplete, reflect that in the order_status.
- Do not claim the order was submitted or paid for.
"""

    # Combine summary instructions with the conversation history
    summary_messages = [
        {
            "role": "system",
            "content": summary_instructions
        }
    ] + context[1:]

    try:
        response = client.chat.completions.create(
            model=MODEL,
            messages=summary_messages,
            temperature=0,
            response_format={"type": "json_object"}
        )

        order_json = response.choices[0].message.content

        # Validate the JSON
        parsed_order = json.loads(order_json)

        # Format the JSON for display
        summary_output.object = (
            "### Order Summary (JSON)\n```json\n"
            + json.dumps(parsed_order, indent=2)
            + "\n```"
        )

    except Exception as error:
        summary_output.object = (
            f"Could not generate the summary: {error}"
        )


summary_button.on_click(generate_order_summary)
```

The `summary_messages` list contains new formatting instructions followed by the existing conversation history, excluding the original system message.

The `response_format` parameter requests a JSON object. `json.loads()` parses the response, and `json.dumps()` formats it for display.

# 6. Assemble the Dashboard

Combine the chat history, input field, buttons, and summary output into a single Panel dashboard.

```python
dashboard = pn.Column(
    pn.pane.Markdown("# OrderBot"),
    pn.pane.Markdown(
        "Welcome! Tell me what you'd like to order."
    ),
    chat_history,
    pn.Row(
        inp,
        chat_button,
        sizing_mode="stretch_width"
    ),
    pn.layout.Divider(),
    summary_button,
    summary_output,
    width=800
)

# Display the chatbot
dashboard.servable()
dashboard
```

# Example Interaction

**Customer:** Hi, I would like to order a pizza.

**OrderBot:** Great! What pizza would you like? We have pepperoni, cheese, and eggplant pizza.

**Customer:** A medium eggplant pizza.

**OrderBot:** Would you like any extra toppings?

**Customer:** No extra toppings.

The conversation continues until the customer has provided the required order details. The summary button can then generate a structured representation of the conversation.

# Example JSON Output

For a single medium cheese pizza with no toppings, the summary could look like this:

```json
{
  "pizza": [
    {
      "item": "Cheese pizza",
      "size": "Medium",
      "quantity": 1,
      "unit_price": 9.25,
      "toppings": [],
      "subtotal": 9.25
    }
  ],
  "drinks": [],
  "sides": [],
  "order_type": "Pickup",
  "delivery_address": null,
  "payment_method": null,
  "total_price": 9.25,
  "currency": "USD",
  "order_status": "Pending confirmation"
}
```

This is an illustrative example of the intended structure, not a guaranteed response from a live API call. The actual summary should reflect the conversation and any missing information.

# Important Implementation Notes

- Install the required dependencies with `pip install openai panel`.
- Set `OPENAI_API_KEY` as an environment variable before running the application. Do not commit API keys to GitHub.
- Run the script with `panel serve filename.py --show` to open it as a Panel application.
- The provided Enter-key handler watches for a newline in the `TextInput` value. Standard Panel text inputs may not include that newline when Enter is pressed, so the handler may need adjustment if Enter does not submit the message.
- The code requests JSON output, but the model's extracted prices and totals should still be checked against the menu before any real order is processed.
- The chatbot does not submit orders to a restaurant system or process payments.

# Skills Demonstrated

- Using the OpenAI Chat Completions API.
- Working with `system`, `user`, and `assistant` message roles.
- Maintaining context across multiple conversation turns.
- Building an interactive interface using Panel.
- Extracting conversational information into JSON.
- Parsing and formatting JSON using Python.
- Handling API errors and missing order information.
- Designing prompts for a specific task and persona.

# Key Takeaway

A custom chatbot combines system instructions, conversation history, model responses, and a user interface. Structured output makes conversational data easier to process, while validation and clear operational boundaries help make the application more reliable.