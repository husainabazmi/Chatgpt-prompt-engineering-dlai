# Iterative Prompt Development

# Objective

Refine prompts through repeated testing to improve output length, relevance, technical accuracy, and formatting.

# Core Concept

Prompt engineering is an iterative process:

Initial Prompt → Evaluate Output → Identify Issues → Refine Instructions → Test Again

The goal is not to find a perfect prompt on the first attempt, but to develop one that meets the application's requirements.

Practical Exercise: Product Description Generation

Task: Generate a product description for a mid-century-inspired office chair using a technical fact sheet.

Input data: Product overview, construction materials, upholstery options, product IDs, and dimensions.

# Iteration 1 — Generate a Product Description

Prompt improvement goal: Establish the task and provide the technical fact sheet as input.

Observation: The generated description was relevant but too long for the intended use.

# Iteration 2 — Control Output Length

Change: Added a character limit of 280 characters.

Observation: The output became more concise and suitable for a product listing.

Learning: Explicit length constraints help control response size, although exact limits may require validation.

# Iteration 3 — Refine the Target Audience

Change: Specified that the description was intended for furniture retailers and should focus on technical details and construction materials.

- Observation: The description emphasized the aluminium base, nylon coating, seat foam, and construction.

- Learning: Defining the target audience changes the content and level of technical detail.

# Iteration 4 — Require Product IDs

Change: Added an instruction to include every seven-character product ID from the fact sheet.

- Observation: The output included both SWC-100 and SWC-110.

- Learning: Explicit requirements improve the likelihood that important product information is included.

# Iteration 5 — Generate Structured HTML

Change: Added requirements to:

Place the description inside a <div> element.

Include a table titled Product Dimensions.

Use two columns: dimension and measurement in inches.

Format the complete output as website-ready HTML.

- Observation: The output contained an HTML product description and a dimensions table.

- Learning: Combining content, formatting, and structural constraints makes model outputs more suitable for integration into applications.

### Final Prompt

""" Your task is to help a marketing team create a product
description for a retail website using a technical fact sheet.

Write a technical description intended for furniture retailers,
focusing on the materials used in the product's construction.

Include every seven-character product ID from the fact sheet
at the end of the description.

After the description, include a two-column table titled
"Product Dimensions". The columns must contain the dimension
name and its measurement in inches only.

Format everything as HTML suitable for a website.
Place the description inside a <div> element. """

Skills Demonstrated

Iterative prompt refinement

Output-length and content constraints

Audience-specific content generation

Extraction of required product identifiers

Structured HTML generation

Converting technical specifications into product content

Key Takeaway

Small, targeted prompt changes can progressively improve an output. For reliable results, test the generated content against explicit requirements, including word or character limits, required identifiers, measurements, and valid HTML structure.