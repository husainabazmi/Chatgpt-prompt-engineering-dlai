# Prompting Guidelines & Practical Examples

# Core Principles

1. Write clear and specific instructions** to guide the model toward the desired output.
2. Give the model time to work through complex tasks** by breaking them into explicit steps and requiring verification before conclusions.

# Prompting Techniques

| Technique | Purpose |
|---|---|
| Delimiters | Separate input text from instructions. |
| Structured output | Specify a predictable format such as JSON. |
| Condition checking | Define how the model should respond when required conditions are not met. |
| Few-shot prompting | Provide examples to guide the response style or format. |
| Step-by-step task instructions | Break complex tasks into smaller, ordered actions. |
| Independent verification | Solve a problem before evaluating another solution. |
| Source-grounded responses | Use relevant source text to reduce unsupported claims. |

# Practical Examples

# Practical Exercises

# 1. Generating Structured JSON

Task: Generate three fictional book titles with their authors and genres.

Prompt:
```text
Generate a list of three made-up book titles along with
their authors and genres. Provide them in JSON format
with the following keys: book_id, title, author, genre.
```

Skills practiced: Structured output, JSON formatting, and following specified field names.

# 2. Converting Text into Steps

Task: Extract instructions from a paragraph and rewrite them in a numbered format.

Example input: A paragraph explaining how to prepare a cup of tea.

Output:
```text
Step 1 - Boil some water.
Step 2 - Grab a cup and put a tea bag in it.
Step 3 - Pour the hot water over the tea bag.
Step 4 - Let the tea steep for a few minutes.
Step 5 - Remove the tea bag.
Step 6 - Add sugar or milk to taste, if desired.
Step 7 - Enjoy your cup of tea.
```

I also tested the same prompt with a descriptive paragraph about sunny weather. Since it contained no sequence of instructions, the expected output was:

```text
No steps provided.
```

Skills practiced: Instruction following, conditional responses, and extracting structured information from text.

# 3. Few-Shot Prompting

Task: Continue a conversation in a consistent style using an example.

Example:
```text
<child>: Teach me about patience.

<grandparent>: The river that carves the deepest valley
flows from a modest spring; the grandest symphony
originates from a single note; the most intricate
tapestry begins with a solitary thread.

<child>: Teach me about resilience.
```

The model generated a response using a similar metaphorical style.

Skills practiced: Few-shot prompting and style imitation through examples.

# 4. Combining Multiple Text Tasks

Task: Summarize a story about Jack and Jill, translate the summary into French, identify names, and return selected information as JSON.

The prompt combined four operations:

1. Summarize the story in one sentence.
2. Translate the summary into French.
3. List the names in the French summary.
4. Return the French summary and name count as JSON.

Skills practiced: Multi-step instructions, translation, information extraction, and structured output.

# 5. Evaluating a Student's Solution

Task: Independently solve a financial calculation before evaluating a student's answer.

The solar installation problem specified:
- Land: $100 per square foot.
- Solar panels: $250 per square foot.
- Maintenance: $100,000 annually plus $10 per square foot.

Let \(x\) represent the installation area in square feet.

The correct total first-year cost is:

\[
C(x)=100x+250x+100{,}000+10x
\]

\[
\boxed{C(x)=360x+100{,}000}
\]

I tested prompts that required the model to calculate the answer first, compare it with the student's solution, and provide a correctness verdict.

**Important learning:** The student's breakdown used the wrong maintenance rate. The final verdict must be based on comparing the student's final expression with the independently calculated result.

# 6. Product Information with Evidence Awareness

Task: Request information about the AeroGlide UltraSlim Smart Toothbrush by Boie.

The response acknowledged that the exact product could not be verified rather than inventing specifications. It then outlined factors to consider when evaluating a toothbrush, including bristles, cleaning technology, smart features, replacement heads, durability, and warranty.

Skills practiced: Recognizing uncertainty, avoiding unsupported product claims, and distinguishing verified information from general evaluation criteria.

## Skills Demonstrated

- Writing clear, specific prompts.
- Requesting structured JSON output.
- Extracting instructions and handling conditional cases.
- Applying few-shot prompting.
- Combining multiple tasks in one prompt.
- Verifying calculations independently.
- Recognizing when information cannot be reliably verified.