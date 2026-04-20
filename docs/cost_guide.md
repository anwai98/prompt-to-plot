# Model Cost Guide

Approximate pricing per 1 million tokens as of early 2026. Prices change — always check the provider's pricing page for the latest.

## Input / Output Token Costs

| Model | Input (per 1M tokens) | Output (per 1M tokens) | Free tier |
|---|---|---|---|
| `gemini-flash-lite-latest` | ~$0.01 | ~$0.04 | Yes |
| `gemini-2.5-flash` | ~$0.15 | ~$0.60 | Yes (low RPM) |
| `gemini-2.5-pro` | ~$1.25 | ~$10.00 | No |
| `claude-haiku-4-5` | ~$0.80 | ~$4.00 | No |
| `claude-sonnet-4-6` | ~$3.00 | ~$15.00 | No |
| `gpt-4o-mini` | ~$0.15 | ~$0.60 | No |
| `gpt-4o` | ~$2.50 | ~$10.00 | No |
| Llama 3 (self-hosted) | Free | Free | N/A |

## How Many Tokens Does One Plot Request Use?

A typical `ask_gemini_to_plot` call in this notebook uses roughly:
- **Input:** ~300–500 tokens (prompt + DataFrame context)
- **Output:** ~200–400 tokens (generated code)

At those sizes, **1000 plot requests costs less than $0.01** on `gemini-flash-lite-latest`.

## Pricing Pages

- Gemini: https://ai.google.dev/pricing
- Claude: https://www.anthropic.com/pricing
- OpenAI: https://openai.com/pricing
