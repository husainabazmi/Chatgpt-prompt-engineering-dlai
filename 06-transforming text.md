# Transforming Text with LLMs

# Objective

Use large language models (LLMs) to transform text into different languages, tones, formats, and writing styles while preserving its intended meaning.

# Key Concepts

- Translation: Convert text from one language to another.
- Language identification: Determine the language of an input message.
- Tone transformation: Rewrite informal or slang text in a professional tone.
- Format conversion: Convert structured data into formats such as HTML.
- Proofreading: Correct spelling, grammar, and punctuation.
- Style transformation: Rewrite content for a specific audience, writing style, or purpose.
- Output constraints: Specify the required format, structure, and response style.

# Practical Exercises

# 1. Multilingual Translation

I practiced translating text into Spanish, French, Hindi, German, and Urdu, as well as generating an English pirate-style response.

Example prompt:
```text
Translate the following text to French and Spanish
and English pirate and Hindi and German and Urdu:

"I want to order a basketball"
```

I also practiced translating the same sentence into both formal and informal Spanish.

Example:
- Formal: ¿Le gustaría pedir una almohada?
- Informal: ¿Te gustaría pedir una almohada?

Learning: Prompts can specify multiple target languages and distinguish between formal and informal language.

# 2. Translating Workplace Policies

Task: Translate a detailed workplace policies document into German.

The document covered:
- Professional behavior and code of conduct
- Attendance and working hours
- Communication and technology usage
- Leave and time-off policies
- Health, safety, and workspace
- Disciplinary actions and grievance procedures

Learning: LLMs can transform lengthy documents while preserving headings, lists, and the original organizational structure. Important translations should still be reviewed for accuracy.

# 3. Transforming Tone: Slang to Business Writing

Input:
```text
Dude, This is Joe, check out this spec on this standing lamp.
```

Prompt:
```text
Translate the following from slang to a business letter.
```

Result:
```text
Dear Sir/Madam,

My name is Joe. Please review the specifications for
this standing lamp at your convenience.

Best regards,
Joe
```

Learning: Specifying the intended tone and format helps adapt a message to a professional audience.

# 4. Converting Python Data to HTML

I used a Python dictionary containing restaurant employees and their email addresses.

Prompt:
```text
Translate the following Python dictionary from JSON
to an HTML table with column headers and title.
```

The generated HTML contained:
- A page title
- A table heading
- Name and email column headers
- Rows for each employee

Learning: LLMs can convert structured data into presentation formats, reducing the need to write custom transformation logic for simple tasks.

# 5. Proofreading and Grammar Correction

I practiced correcting spelling, punctuation, subject–verb agreement, and commonly confused words.

Examples from my practice:

| Original | Corrected |
|---|---|
| The girl with the black and white puppies have a ball. | The girl with the black and white puppies has a ball. |
| Its going to be a long day. | It's going to be a long day. |
| Their goes my freedom. | There goes my freedom. |
| Your going to need you're notebook. | You're going to need your notebook. |
| That medicine effects my ability to sleep. | That medicine affects my ability to sleep. |
| This phrase is to cherck chatGPT for speling abilitty. | This phrase is to check ChatGPT for spelling ability. |

I also specified that the model should return the corrected version without additional punctuation around the text.

Learning: Explicit output instructions help make proofreading results more consistent and easier to reuse.

# 6. Rewriting a Product Review

I used a panda plush toy review to practice more advanced editing.

Initial task: Proofread and correct the review.

Advanced task: Proofread and correct the review, make it more compelling, follow APA style guidance, target an advanced reader, and output in Markdown.

The final output included:
- A descriptive heading
- Improved sentence structure
- More formal vocabulary
- Clearer discussion of product strengths and weaknesses
- Markdown formatting

Learning: A prompt can request more than grammatical correction. It can also specify the audience, tone, writing style, and output format.

# Skills Demonstrated

- Multilingual text transformation
- Language identification
- Formal and informal tone control
- Professional writing
- Python dictionary-to-HTML conversion
- Grammar and spelling correction
- Markdown formatting
- Audience-aware rewriting
- Prompt design with explicit output constraints

# Key Takeaway

Text transformation prompts should specify both the desired change and the required output. Whether translating languages, correcting grammar, changing tone, or converting formats, clear constraints help produce more useful and consistent results.