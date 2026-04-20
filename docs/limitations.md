# Limitations of LLM-Generated Plotting Code

LLMs are good at generating plotting code but not perfect. Here are the most common failure modes and how to handle them.

## 1. Hallucinated function arguments

The LLM may pass arguments that don't exist in the library.

**Example:** `sns.regplot(..., hue='group')` — `regplot` does not support `hue`.

**Fix:** Be explicit in your prompt — "use `sns.lmplot` for regression lines per group, not `sns.regplot`".

---

## 2. Deprecated APIs

LLMs are trained on older code and may use functions that have been removed or renamed.

**Example:** `plt.cm.get_cmap()` was deprecated in matplotlib 3.7 in favour of `matplotlib.colormaps[]`.

**Fix:** The auto-fix mechanism in this notebook will usually catch and correct these. If not, add "use the latest matplotlib API" to your prompt.

---

## 3. Wrong columns used

The LLM may pick a plausible-sounding column that doesn't exist or use the wrong one.

**Fix:** Always name the exact column in your prompt — "use the `exam_score` column, not `score`".

---

## 4. Subtly wrong visualisations

The plot runs without error but shows the wrong thing — e.g. a mean instead of a median, or unsorted categories.

**Fix:** Be explicit — "sort the x-axis from A to D" or "show the median, not the mean". Always inspect the output.

---

## 5. Mixed libraries

The LLM may import a library you didn't ask for or mix matplotlib and plotly calls in the same block.

**Fix:** Always pass `library_hint` to constrain the model to one library.

---

## 6. Overly complex code

The LLM sometimes generates unnecessarily verbose or convoluted code for a simple chart.

**Fix:** Add "keep the code as simple as possible" to your prompt.

---

## 8. Hallucinated column names

The LLM may invent a plausible-sounding column name that doesn't exist in your DataFrame.

**Example:** Your DataFrame has `log2_fold_change` but the LLM writes `log2fc`.

**Fix:** Always run `df.columns.tolist()` before prompting and paste the exact names into your request — "use the column named `log2_fold_change`, not `log2fc`". The notebook sends column names automatically, but being explicit in the prompt removes ambiguity.

---

## 7. Plotly not rendering in Colab

Plotly charts sometimes appear blank in Google Colab, especially with `fig.show()`.

**Fix:** Use the Colab-compatible renderer explicitly:

```python
import plotly.io as pio
pio.renderers.default = 'colab'
fig.show()
```

Or save to HTML and download:

```python
fig.write_html('plot.html')
from google.colab import files
files.download('plot.html')
```

If you ask Gemini for a plotly chart and the output is blank, add "set `pio.renderers.default = 'colab'` before calling `fig.show()`" to your prompt.

---

## 9. Non-determinism

Running the same prompt twice may produce different code. This is normal — LLMs are probabilistic. If one run produces a bad plot, just re-run the cell.
