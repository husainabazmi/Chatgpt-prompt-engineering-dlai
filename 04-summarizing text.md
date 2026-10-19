# Summarizing Text with LLMs

# Objective

Use large language models (LLMs) to summarize lengthy text, customize summaries for specific business needs, extract relevant information, and process multiple reviews efficiently.

# Key Concepts

- Length-controlled summaries: Limit the summary by word count or sentence count.
- Audience-specific summaries: Focus on information relevant to a particular department.
- Information extraction: Extract only the requested details instead of summarizing the entire text.
- Batch processing: Loop through multiple reviews and generate a concise summary for each one.

# Practical Exercises

# 1. Summarizing a Product Review

Task: Summarize an e-commerce review in at most 30 words.

Prompt:
```text
Your task is to generate a short summary of a product
review from an ecommerce site.

Summarize the review below, delimited by triple
backticks, in at most 30 words.
```

Result: The panda plush is soft, cute, and friendly-looking, making it a hit with the daughter. It arrived early but feels smaller than expected for its price.

# 2. Creating Department-Specific Summaries

The same review can be summarized differently depending on the intended audience.

Shipping department: Focus on shipping and delivery.

> The product arrived one day earlier than expected, providing a faster-than-anticipated delivery experience.

Pricing department: Focus on price and perceived value.

> The customer finds the panda plush cute and soft but considers it too small for the price, suggesting larger alternatives may offer better value.

Key learning: Specify the audience and purpose in the prompt to make the output more relevant.

# 3. Extracting Relevant Information

Instead of summarizing the whole review, extract only the information needed by the shipping department.

Prompt:
```text
Your task is to extract relevant information from
a product review from an ecommerce site to give
feedback to the Shipping department.

From the review below, delimited by triple quotes,
extract the information relevant to shipping and
delivery. Limit to 30 words.
```

Result: The product arrived one day earlier than expected, providing a faster-than-anticipated delivery experience.

Key learning: Summarization condenses the overall content, while extraction returns only information relevant to a specific requirement.

# 4. Summarizing Multiple Reviews with Python

I prepared four product reviews covering a panda plush toy, standing lamp, electric toothbrush, and blender.

The reviews were stored in a list and processed using a `for` loop.

```python
reviews = [review_1, review_2, review_3, review_4]

for i in range(len(reviews)):
    prompt = f"""
    Your task is to generate a short summary of a product
    review from an ecommerce site.

    Summarize the review below, delimited by triple
    backticks in at most 20 words.

    Review: ```{reviews[i]}```
    """

    response = get_completion(prompt)
    print(i, response, "\n")
```

# How it works:
1. Store the reviews in a list.
2. Iterate through the list using a `for` loop.
3. Insert the current review into the prompt using an f-string.
4. Call `get_completion()` to generate a summary.
5. Print the review index and its summary.

This approach can be extended to summarize large collections of customer reviews for dashboards and customer-feedback analysis.

# Skills Demonstrated

- Prompt design for concise summaries
- Word-count constraints
- Audience-specific prompt customization
- Information extraction
- Python lists, loops, and f-strings
- Reusing a completion function to process multiple text inputs

## Key Takeaway

A good summarization prompt specifies the desired length, purpose, and relevant information.** Combining prompting with Python loops makes it possible to process multiple reviews efficiently.