# Inferring Information from Text with LLMs

# Objective

Use large language models (LLMs) to analyze text and infer information such as sentiment, emotions, product details, and topics without training a separate model for each task.

# Key Concepts

- Sentiment analysis: Classify text as positive or negative.
- Emotion detection: Identify emotions such as anger from written reviews.
- Information extraction: Extract specific details, such as product names and brands.
- Structured output: Format extracted information as JSON for further processing.
- Topic identification: Determine the main topics discussed in a text.
- Zero-shot classification: Classify text against predefined topics using instructions without providing labeled training examples.

# Practical Exercises

# 1. Detecting Anger

Task:** Determine whether a customer review expresses anger.

Prompt:
```text
Is the writer of the following review expressing anger?
The review is delimited with triple backticks.
Give your answer as either yes or no.
```

Result:
```text
no
```

Learning: A prompt can classify an emotional characteristic using a simple yes/no response.

# 2. Extracting Product and Brand

Task: Identify the purchased item and the company that made it.

Prompt requirements:
- Extract the item and brand.
- Return a JSON object with `Item` and `Brand` keys.
- Use `"unknown"` when information is unavailable.

Result:
```json
{
  "Item": "lamp",
  "Brand": "Lumina"
}
```

Learning: Structured JSON output makes information easier to process programmatically.

# 3. Extracting Multiple Fields in One Prompt

Instead of making separate API calls, I combined multiple inference tasks into one prompt.

Fields extracted:
- Sentiment
- Anger detection
- Purchased item
- Brand

Result:
```json
{
  "Sentiment": "positive",
  "Anger": false,
  "Item": "lamp",
  "Brand": "Lumina"
}
```

Learning: A single well-defined prompt can extract multiple fields, including a Boolean value, from the same review.

# 4. Identifying Topics in an Article

Task: Identify five topics from a fictional government employee satisfaction survey article.

Prompt requirements:
- Generate five topics.
- Keep each topic to one or two words.
- Return a comma-separated list.

Result:
```text
employee satisfaction, NASA, government survey,
workplace environment, Social Security Administration
```

I also practiced converting the comma-separated response into a Python list.

```python
response.split(sep=", ")
```

This separates the topics into individual list elements.

# 5. Classifying an Article Against Predefined Topics

Task: Determine which predefined topics appear in the article.

```python
topic_list = [
    "nasa",
    "local government",
    "engineering",
    "employee satisfaction",
    "federal government"
]
```

I used an f-string to insert the topics into the prompt:

```python
List of topics: {", ".join(topic_list)}
```

Result:
```text
nasa: 1
local government: 0
engineering: 0
employee satisfaction: 1
federal government: 1
```

Here, `1` indicates that a topic is present, while `0` indicates that it is absent.

Learning: A language model can classify text against a predefined topic list without task-specific labeled training examples. For more reliable programmatic processing, structured JSON output can be requested instead of a loosely formatted list.

# Skills Demonstrated

- Sentiment classification
- Emotion and anger detection
- Information extraction from reviews
- JSON-formatted output
- Python string splitting and f-strings
- Topic identification and zero-shot classification
- Combining multiple inference tasks in one prompt

# Key Takeaway

Clear prompts can turn unstructured text into useful, structured information. By specifying the fields, output format, and classification rules, LLMs can support multiple text-analysis tasks through a single model and API.