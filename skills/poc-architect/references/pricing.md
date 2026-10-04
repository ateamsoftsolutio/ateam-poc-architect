# Fallback model prices

Use this table only when a live lookup of the providers' official pricing pages fails. Say that the fallback was used and give its date. Update this file whenever prices change.

Fallback table (list prices per million tokens, input / output, checked 26 September 2026):

| Tier | Anthropic | OpenAI |
|---|---|---|
| Small | Claude Haiku 4.5: $1 / $5 | GPT-6 Luna: $0.10 / $0.50 |
| Mid | Claude Sonnet 5: $2 / $10 | GPT-6 Sol: $2 / $10 |
| Large | Claude Opus 5.5: $4 / $20 | GPT-6 Astra: $10 / $50 |

- Both providers discount batch processing by 50%.
- Cached input is about 10% of the input price (Opus 5.5 cache reads are 5%).
- OpenAI long-context variants cost twice the standard price.
- Claude Sonnet 5 and Opus 5.5 count roughly 30% more tokens than Haiku 4.5 for the same text.

Official pricing pages:
- Anthropic: https://platform.claude.com/docs/en/about-claude/pricing
- OpenAI: https://developers.openai.com/api/docs/pricing
