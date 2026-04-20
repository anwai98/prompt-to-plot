# LLM Models for Code Generation

A reference for the most popular LLMs you can use for generating plotting code.

---

## Gemini (Google)

| Model | Free tier | Context window | Best for |
|---|---|---|---|
| `gemini-flash-lite-latest` | Yes | 1M tokens | Quick code generation, high rate limits |
| `gemini-2.5-flash-lite` | Yes | 1M tokens | Same as above, explicit version |
| `gemini-2.5-flash` | Yes (low RPM) | 1M tokens | Higher quality output than lite |
| `gemini-2.5-pro` | No | 1M tokens | Complex multi-step reasoning |
| `gemini-3-flash-preview` | No | 1M tokens | Next-gen flash model |

**Used in this notebook.** Access via [Google AI Studio](https://aistudio.google.com/app/apikey).
Rate limits and pricing: https://ai.google.dev/pricing

---

## Claude (Anthropic)

| Model | Context window | Best for |
|---|---|---|
| `claude-haiku-4-5` | 200K tokens | Fast, cheap, good for simple code tasks |
| `claude-sonnet-4-6` | 200K tokens | Best balance of quality and speed |
| `claude-opus-4-7` | 200K tokens | Most capable, complex reasoning |
| `claude-3-5-haiku-20241022` | 200K tokens | Previous generation, very fast |
| `claude-3-5-sonnet-20241022` | 200K tokens | Previous generation, highly capable |
| `claude-3-opus-20240229` | 200K tokens | Previous generation, top quality |
| `claude-3-haiku-20240307` | 200K tokens | Previous generation, lightweight |

Strong at following detailed instructions and writing clean, idiomatic Python. Excellent for complex, multi-step visualisation tasks.
Access via [Anthropic Console](https://console.anthropic.com/).
Pricing: https://www.anthropic.com/pricing

---

## GPT (OpenAI)

| Model | Context window | Best for |
|---|---|---|
| `gpt-4o-mini` | 128K tokens | Fast, cheap code generation |
| `gpt-4o` | 128K tokens | High quality output |
| `gpt-4-turbo` | 128K tokens | Previous generation, strong at code |
| `gpt-3.5-turbo` | 16K tokens | Very cheap, simple tasks only |
| `o1-mini` | 128K tokens | Reasoning-focused, slower |
| `o3-mini` | 200K tokens | Advanced reasoning |

Very capable at code generation, large ecosystem of examples.
Access via [OpenAI Platform](https://platform.openai.com/).
Pricing: https://openai.com/pricing

---

## Llama (Meta — Open Source)

| Model | Parameters | Best for |
|---|---|---|
| `llama-3.3-70b` | 70B | High quality, needs GPU |
| `llama-3.2-11b` | 11B | Good balance, mid-range GPU |
| `llama-3.2-3b` | 3B | Lightweight, CPU-friendly |
| `llama-3.1-8b` | 8B | Good general purpose |
| `codellama-34b` | 34B | Code-specific tasks |

Fully open source — can be run locally via [Ollama](https://ollama.com/) or accessed through providers:
- [Groq](https://groq.com/) — free tier, very fast inference
- [Together AI](https://www.together.ai/) — affordable hosted inference
- [Hugging Face](https://huggingface.co/inference-api) — free tier available

---

## Mistral (Open Source)

| Model | Context window | Best for |
|---|---|---|
| `mistral-small-latest` | 32K tokens | Lightweight general tasks |
| `mistral-large-latest` | 128K tokens | High quality output |
| `codestral-latest` | 256K tokens | Code-specific model |
| `mistral-nemo` | 128K tokens | Open weights, self-hostable |

`codestral` is specifically trained on code and performs well on plotting tasks.
Access via [Mistral Platform](https://console.mistral.ai/).

---

## Gemma (Google — Open Source)

| Model | Parameters | Best for |
|---|---|---|
| `gemma-3-27b-it` | 27B | High quality, instruction-tuned |
| `gemma-3-12b-it` | 12B | Good balance |
| `gemma-3-4b-it` | 4B | Lightweight, fast |
| `gemma-3-1b-it` | 1B | Minimal compute |

Open weights from Google, available via the Gemini API (free tier) and self-hostable via Ollama or Hugging Face.

---

## Choosing a Model

| Goal | Recommendation |
|---|---|
| Free, no setup | `gemini-flash-lite-latest` |
| Best code quality | `claude-sonnet-4-6` or `gpt-4o` |
| Fully offline / private data | Llama 3 via Ollama |
| Code-specific tasks | `codestral-latest` |
| Large context (big DataFrames) | Any Gemini or Claude model |
| Cheapest paid option | `gpt-4o-mini` or `claude-haiku-4-5` |
