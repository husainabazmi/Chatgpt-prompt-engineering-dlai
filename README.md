# ChatGPT Prompt Engineering for Developers — DeepLearning.AI

My progress and notes while working through the [ChatGPT Prompt Engineering for Developers](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers-with-openai/) short course by DeepLearning.AI.

## About the Course
A short course covering best practices for prompting large language models (LLMs) using the OpenAI API — writing clear instructions, giving the model time to think, iterative prompting, summarizing, inferring, transforming, and expanding text.

## Progress

| Lesson | Topic | Status |
|--------|-------|--------|
| 1 | Guidelines for Prompting | ✅ Done |
| 2 | Iterative Prompt Development | ✅ Done |
| 3 | Summarizing | 🔲 In progress |
| 4 | Inferring | 🔲 Not started |
| 5 | Transforming | 🔲 Not started |
| 6 | Expanding | 🔲 Not started |
| 7 | Chatbot | 🔲 Not started |

## What's in this repo
- `01-guidelines/` — notebook + notes on prompting principles
- `02-iterative-prompting/` — examples of refining prompts step by step

## Key Takeaways
- Be specific and give the model clear, structured instructions
- Use delimiters to separate instructions from content
- Ask for structured output (e.g. JSON) when you need to parse results

## Setup
This course uses the OpenAI API. To run these notebooks:
1. Clone this repo
2. Install dependencies: `pip install openai python-dotenv`
3. Add your OpenAI API key to a `.env` file (not committed — see `.gitignore`)
