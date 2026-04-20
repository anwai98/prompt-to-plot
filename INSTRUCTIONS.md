# Instructions

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/anwai98/prompt-to-plot/blob/main/llm_plotting_with_gemini.ipynb)

## Running in Google Colab (recommended)

1. Get a free Gemini API key from [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Open the notebook in Colab using the badge in the README
3. In the left sidebar, click the **🔑 icon → Add new secret**
   - Name: `GEMINI_API_KEY`, Value: your key, toggle **Notebook access** on
4. Run cells one by one using **Shift + Enter**

---

## Running locally

1. Clone the repo and install dependencies:

   ```bash
   git clone https://github.com/anwai98/prompt-to-plot
   cd prompt-to-plot
   pip install jupyter google-genai pandas matplotlib seaborn plotly
   ```

2. Set your API key as an environment variable:

   ```bash
   export GEMINI_API_KEY=your-api-key
   ```

3. In the setup cell, replace the Colab Secrets line with:

   ```python
   import os
   api_key = os.environ['GEMINI_API_KEY']
   client = genai.Client(api_key=api_key)
   ```

4. Launch Jupyter and open the notebook:

   ```bash
   jupyter notebook llm_plotting_with_gemini.ipynb
   ```
