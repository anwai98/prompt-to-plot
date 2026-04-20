# Switching to a Different LLM

The notebook's helper functions are model-agnostic. Only the setup cell needs to change when using the API. For UI and CLI tools, a different workflow applies — no code changes needed.

---

## Option A: API-Based (run code in Colab)

### Switching to Claude (Anthropic)

```python
!pip install -q anthropic

import anthropic

anthropic_client = anthropic.Anthropic(api_key='your-api-key')

def call_gemini(prompt):  # rename if you like
    for attempt in range(5):
        try:
            message = anthropic_client.messages.create(
                model='claude-haiku-4-5',
                max_tokens=1024,
                messages=[{'role': 'user', 'content': prompt}]
            )
            return message.content[0].text
        except anthropic.RateLimitError:
            print(f'Rate limit hit, retrying {attempt + 1}/5...')
            time.sleep(60)
    return None
```

Then update `ask_gemini_to_plot` to call `call_gemini(prompt)` and use the returned string directly instead of `response.text`.

---

### Switching to GPT-4o (OpenAI)

```python
!pip install -q openai

from openai import OpenAI

openai_client = OpenAI(api_key='your-api-key')

def call_gemini(prompt):
    for attempt in range(5):
        try:
            response = openai_client.chat.completions.create(
                model='gpt-4o-mini',
                messages=[{'role': 'user', 'content': prompt}]
            )
            return response.choices[0].message.content
        except Exception as e:
            if '429' in str(e):
                print(f'Rate limit hit, retrying {attempt + 1}/5...')
                time.sleep(60)
            else:
                raise
    return None
```

---

### Switching to Llama (via Ollama, fully local)

```python
!pip install -q ollama

import ollama

def call_gemini(prompt):
    response = ollama.chat(
        model='llama3.3',
        messages=[{'role': 'user', 'content': prompt}]
    )
    return response['message']['content']
```

Requires [Ollama](https://ollama.com/) installed and running locally. No API key needed.

---

### What Stays the Same

`build_prompt`, `extract_code`, `ask_gemini_to_plot`, and all plotting examples work unchanged across all models — only the `call_gemini` function needs to be swapped out.

---

## Option B: Web UI (no code required)

You can use any LLM chat interface to generate plotting code without touching the notebook infrastructure. This is the simplest approach if you just want a one-off plot.

### Workflow

1. Run `build_prompt(df, 'df', 'your request')` in Colab to generate the prompt string.
2. Copy the output.
3. Paste it into the chat interface of your choice.
4. Copy the returned code block back into a Colab cell and run it.

### ChatGPT (OpenAI) — chat.openai.com

- Free tier available (`gpt-4o-mini` by default).
- Paste the prompt and ask for a self-contained Python code block.
- GPT-4o is available on the paid plan and produces higher-quality code.

### Claude.ai (Anthropic) — claude.ai

- Free tier available (Claude Sonnet).
- Handles long prompts well; good at following detailed formatting instructions.
- Pro plan unlocks Claude Opus for more complex multi-step plots.

### Gemini (Google) — gemini.google.com

- Free with a Google account.
- Can also run the code directly inside a connected Google Colab via the Gemini side panel.
- Use the side panel: open your notebook, click the Gemini icon (top right), and paste your prompt there — it can insert code directly into a cell.

### Tips for UI-based prompting

- Always ask for a **self-contained code block** that imports its own libraries.
- Specify the plotting library explicitly: "Use seaborn", "Use plotly", etc.
- If the code fails, paste the error message back into the chat and ask for a fix.

---

## Option C: Claude Code CLI

[Claude Code](https://claude.ai/code) is Anthropic's terminal-based AI assistant. It can write and iterate on plotting scripts directly from your local environment.

### Setup

```bash
npm install -g @anthropic-ai/claude-code
claude  # opens an interactive session
```

Requires an Anthropic API key set as `ANTHROPIC_API_KEY`.

### Workflow

Instead of running the notebook, work in a `.py` script or a local Jupyter notebook:

```
You: I have a pandas DataFrame called df with columns: gene, log2fc (float), pvalue (float), cell_type (str).
     Write a seaborn volcano plot: x=log2fc, y=-log10(pvalue), colored by cell_type.
     Make it self-contained with all imports.
```

Claude Code can:
- Write the full script from a description of your data and goal.
- Read an existing script or notebook and modify it.
- Run the script in the terminal and fix errors automatically (`/run`).
- Iterate across multiple files in a project.

### Running inside a notebook

Use Claude Code from the terminal alongside an open Jupyter session:
1. Start `jupyter notebook` in one terminal.
2. Run `claude` in a second terminal in the same directory.
3. Ask Claude Code to edit the notebook file directly.

---

## Option D: GitHub Copilot / Codex (in-IDE)

GitHub Copilot integrates into VS Code, JetBrains, and other editors. It generates code inline as you type, making it useful for iterating on plots without leaving your editor.

### Setup

- Install the [GitHub Copilot extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) in VS Code.
- Sign in with a GitHub account (free trial available, then paid).
- Open a `.py` file or a `.ipynb` file (Jupyter extension required).

### Workflow

Write a comment describing the plot and let Copilot complete the code:

```python
# Seaborn scatter plot of log2fc vs -log10(pvalue), colored by cell_type, with significance threshold lines
```

Copilot will suggest a full code block. Press `Tab` to accept.

For more control, use **Copilot Chat** (the chat panel in VS Code):
- Describe your DataFrame and ask for a complete plotting function.
- Paste an error message and ask for a fix.
- Ask it to convert a matplotlib plot to plotly.

### GitHub Copilot in Jupyter (VS Code)

If you open the main notebook in VS Code with the Jupyter extension:
- Inline completions work inside code cells.
- Copilot Chat can explain a cell, rewrite it, or generate a new one based on a description.

### OpenAI Codex (API)

Codex is the model underlying older Copilot versions and is accessible via the OpenAI API. Use `gpt-4o` or `gpt-4o-mini` with a system prompt that enforces Python plotting conventions — the API approach in Option A covers this use case.

---

## Comparison

| Method | Setup effort | Cost | Best for |
|---|---|---|---|
| Gemini API (default) | Low | Free tier | Running everything in Colab |
| Claude / OpenAI API | Low | Paid | Higher quality output in Colab |
| Ollama (local) | Medium | Free | Private data, no internet |
| Web UI (ChatGPT / Claude.ai) | None | Free tier | One-off plots, no coding |
| Claude Code CLI | Low | Paid | Iterative local development |
| GitHub Copilot | Low | Paid | In-editor, inline suggestions |
