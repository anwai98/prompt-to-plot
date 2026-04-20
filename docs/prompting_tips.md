# Prompting Strategies for Plot Generation

Getting good plots out of an LLM comes down to giving it enough context and being specific about what you want.

## The Golden Rule

**Be as specific as you would be if describing the plot to a colleague who will code it for you.**

---

## 1. Always Specify the Library

Without a library hint, the LLM may pick one you don't want or mix libraries.

| Vague | Specific |
|---|---|
| "plot the data" | "Plot the data using matplotlib" |
| "show a chart" | "Create a seaborn box plot" |

---

## 2. Name Your Axes Explicitly

| Vague | Specific |
|---|---|
| "scatter plot of the data" | "Scatter plot: x = gdp_per_capita, y = life_expectancy" |
| "show sales over time" | "Line chart: x = Month, y = Total" |

---

## 3. Describe Visual Encodings

Tell the LLM how to use color, size, and shape.

- "Color points by `continent`"
- "Size bubbles by `population_M`"
- "Use a distinct color per `grade_group`"
- "Use a red-blue diverging palette centered at 0"

---

## 4. Specify Axis Transformations

| Example |
|---|
| "Use a log scale on the x-axis" |
| "Normalise the y-axis from 0 to 1" |
| "Sort the x-axis from highest to lowest" |

---

## 5. Ask for Annotations

LLMs are good at adding contextual annotations when asked:

- "Add a vertical dashed line at the mean"
- "Label the top 5 points with their gene name"
- "Mark the maximum value with a red dot and annotate it"
- "Add a linear regression trend line per group"

---

## 6. Describe the Data Transformation

If the plot requires aggregation or filtering, say so explicitly:

- "Group by continent and take the mean GDP"
- "Filter to only show significant genes (significant == True)"
- "Compute the correlation matrix first, then plot it as a heatmap"

---

## 7. Iterative Refinement

Start simple and build up:

1. "Create a scatter plot of x vs y"
2. "Color the points by category"
3. "Add a trend line and make the axes log scale"
4. "Add hover tooltips showing the exact values"

Each step is a new prompt — you don't need to ask for everything at once.

---

## 8. Common Prompt Templates

**Distribution plot:**
> "Show the distribution of `[column]` as a histogram with 20 bins and a KDE overlay. Add a dashed line at the mean. Use seaborn."

**Comparison across groups:**
> "Create a box plot comparing `[column]` across `[group_column]`. Order groups as `[A, B, C]`. Color each group differently. Use seaborn."

**Relationship between two variables:**
> "Scatter plot of `[x]` vs `[y]`, colored by `[category]`. Add a regression line per group. Use seaborn."

**Time series:**
> "Line chart of `[y]` over `[time_column]`. Mark the maximum with a red dot and annotate it. Use matplotlib."

**Interactive exploration:**
> "Interactive scatter plot: x = `[x]`, y = `[y]`, color = `[category]`, size = `[size_col]`. Add hover tooltips showing all columns. Use plotly."

---

## 9. Gene Expression / Bioinformatics Prompts

These datasets have conventions worth spelling out explicitly.

**Volcano plot:**
> "Scatter plot: x = `log2fc`, y = `-log10(pvalue)`. Color points red if `significant == True`, grey otherwise. Add dashed horizontal line at y = 1.3 (p = 0.05) and vertical lines at x = ±1. Label the top 5 significant genes by absolute `log2fc` with their `gene` name. Use matplotlib."

**Heatmap of gene expression:**
> "Heatmap of the expression matrix. Rows = genes, columns = samples. Use a red-blue diverging colormap centered at 0. Add row and column labels. Cluster rows by similarity. Use seaborn."

**MA plot:**
> "Scatter plot: x = mean expression (`baseMean`, log scale), y = `log2fc`. Color points by `significant`. Add a horizontal line at y = 0. Use matplotlib."

**Gene expression across cell types:**
> "Box plot of expression level for each `cell_type`. Overlay individual data points as a strip plot. Sort cell types by median expression descending. Use seaborn."

**Tip:** If your DataFrame has a `gene` or `gene_name` column, mention it explicitly so the LLM uses it for labels rather than the row index.

---

## 10. What to Do When the Plot is Wrong

- **Wrong chart type**: Be more explicit — "I want a BAR chart, not a line chart"
- **Wrong columns used**: Name the exact column — "Use `exam_score`, not `assignments`"
- **Style issues**: Describe what you want — "Make the font larger" or "Use a white background"
- **Code error**: Re-run the cell — the notebook will send the error back to Gemini automatically
