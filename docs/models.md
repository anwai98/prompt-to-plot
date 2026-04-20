# LLM Models for Code Generation

A quick reference for the most popular LLMs you can use for generating plotting code.

## Gemini (Google)

| Model | Free tier | Best for |
|---|---|---|
| `gemini-flash-lite-latest` | Yes | Quick code generation, high rate limits |
| `gemini-2.5-flash` | Yes (low RPM) | Higher quality output than lite |
| `gemini-2.5-pro` | No | Complex, multi-step reasoning |

**Used in this notebook.** Access via [Google AI Studio](https://aistudio.google.com/app/apikey).

---

## Claude (Anthropic)

| Model | Free tier | Best for |
|---|---|---|
| `claude-haiku-4-5` | No | Fast, cheap code generation |
| `claude-sonnet-4-6` | No | High quality code, strong reasoning |
| `claude-opus-4-7` | No | Most capable, complex tasks |

Strong at following detailed instructions and writing clean, idiomatic Python. Access via [Anthropic Console](https://console.anthropic.com/).

---

## GPT (OpenAI)

| Model | Free tier | Best for |
|---|---|---|
| `gpt-4o-mini` | No (cheap) | Fast code generation |
| `gpt-4o` | No | High quality output |

Very capable at code generation. Access via [OpenAI Platform](https://platform.openai.com/).

---

## Llama (Meta — Open Source)

| Model | Free tier | Best for |
|---|---|---|
| `llama-3.3-70b` | Self-hosted | Offline / private use |
| `llama-3.2-3b` | Self-hosted | Lightweight, fast inference |

Fully open source — can be run locally via [Ollama](https://ollama.com/) or accessed through providers like [Groq](https://groq.com/) (free tier available).

---

## Mistral (Open Source)

| Model | Free tier | Best for |
|---|---|---|
| `mistral-small` | Via API | Lightweight code tasks |
| `codestral` | Via API | Code-specific model |

`codestral` is specifically trained on code and performs well on plotting tasks. Access via [Mistral Platform](https://console.mistral.ai/).

---

## Choosing a Model

- **For this notebook**: `gemini-flash-lite-latest` — free, no billing setup required.
- **Best code quality**: Claude Sonnet or GPT-4o.
- **Fully offline / private data**: Llama 3 via Ollama.
- **Code-specific tasks**: Codestral.
