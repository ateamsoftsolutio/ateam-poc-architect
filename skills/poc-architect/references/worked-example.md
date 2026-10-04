# Worked example: email intake


| Step | Level | Tokens |
|---|---|---|
| New email arrives via webhook | Code | 0 |
| Strip noise; parse and OCR attachments | Code or local OCR | 0 |
| Detect intent; extract fields to JSON | Small model | about 6,000 in, 300 out |
| Route by intent | Code | 0 |
| Complex or low-confidence cases only | Mid model | a small share of emails |
| Act; a human approves customer replies | Code | 0 |

At the fallback list prices, the small-tier step costs about $7.50 per 1,000 emails on Haiku 4.5, or about $0.75 on GPT-6 Luna. The same use case built as one agent that loops over the full thread on a large model can cost roughly a hundred times more. Always show which of the two the design is closer to.
