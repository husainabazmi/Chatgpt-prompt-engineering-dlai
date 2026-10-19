# 07. Expanding Text with LLMs

# Objective
Learn how to use large language models (LLMs) to expand short inputs into longer, personalized text, such as customer service emails, while controlling the tone, length, and creativity of the output.

# Key Concepts

- Text expansion: Generating longer content from shorter inputs, such as turning a customer review and its sentiment into a personalized email.
- Conditional instructions: Changing the response according to the sentiment. For negative reviews, apologize and suggest contacting customer service; for positive or neutral reviews, express appreciation.
- Personalization: Using specific details from a review and a customer's name to make the response more relevant.
- Tone and length control:** Asking the model to write professionally, keep the email concise, or shorten an existing response.
- Transparency: Clearly identifying AI-generated customer service messages as written by an AI assistant.
- Temperature: A parameter that influences the variety of generated responses. Lower temperature generally produces more predictable outputs, while higher temperature allows more variation.

# Practical Exercises

# 1. Generating Replies to Negative Reviews

Used refrigerator reviews describing recurring cooling problems and a separate delivery complaint involving delays, careless handling, and a dent.

The prompts instructed the model to:
- Apologize for the customer's experience.
- Mention specific details from the review.
- Suggest contacting customer service.
- Maintain a concise, professional tone.
- Sign the email as `AI customer agent`.

# 2. Generating Replies to Positive Reviews

Created personalized thank-you emails for fragrance reviews covering scent, longevity, affordability, and everyday use.

The generated responses acknowledged details such as:
- A fragrance's fresh, ocean-inspired scent.
- Its approximate eight-hour longevity.
- Its value for money.
- Feedback about a spray nozzle.

# 3. Shortening an Email

Asked the model to shorten a thank-you email while preserving the main message, appreciation, and product-specific feedback.

# 4. Personalizing the Greeting

Modified the shortened email to address the customer by name, demonstrating how an additional input can personalize generated content.

# Skills Demonstrated

- Generating text from structured instructions and short inputs.
- Using sentiment to control the response.
- Personalizing customer service emails.
- Maintaining a professional tone and concise writing style.
- Refining generated content through follow-up prompts.
- Understanding how temperature affects output variability.

# Key Takeaway

LLMs can expand short inputs into useful, context-aware content. Clear instructions, sentiment-based conditions, specific review details, and iterative refinement help produce more relevant responses. Temperature can be adjusted depending on whether predictable or more varied outputs are desired.

Responsible use also matters: generated messages should be transparent about AI involvement and should help users rather than enable spam.