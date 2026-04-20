# Python Plotting Libraries

A guide to the three libraries used in this notebook.

---

## Matplotlib

The foundational Python plotting library. Almost every other library builds on top of it.

**Best for:** Publication-quality static figures, full control over every visual detail.

**Install:** `pip install matplotlib`

**Official docs:** https://matplotlib.org/stable/

**Beginner tutorial:** https://matplotlib.org/stable/tutorials/introductory/pyplot.html

### Plot types

| Plot | Function | Use case |
|---|---|---|
| Line chart | `plt.plot()` | Trends over time |
| Bar chart | `plt.bar()` / `plt.barh()` | Comparing categories |
| Scatter plot | `plt.scatter()` | Relationships between variables |
| Histogram | `plt.hist()` | Distributions |
| Box plot | `plt.boxplot()` | Distribution + outliers per group |
| Heatmap | `plt.imshow()` | 2D matrix data |
| Pie chart | `plt.pie()` | Part-to-whole (use sparingly) |
| Error bars | `plt.errorbar()` | Mean ± std or confidence intervals |

### When to use matplotlib

- You need precise control over figure layout, fonts, or spacing
- You are producing figures for a paper or report
- You need a specific chart type not available in seaborn/plotly
- You want to combine multiple subplots in a complex layout

---

## Seaborn

A statistical visualisation library built on matplotlib. Handles grouping, aggregation, and distribution plots with minimal code.

**Best for:** Statistical plots, comparing distributions across groups, correlation analysis.

**Install:** `pip install seaborn`

**Official docs:** https://seaborn.pydata.org/

**Tutorial gallery:** https://seaborn.pydata.org/examples/index.html

### Plot types

| Plot | Function | Use case |
|---|---|---|
| Histogram + KDE | `sns.histplot()` | Distribution of a single variable |
| KDE only | `sns.kdeplot()` | Smooth density estimate |
| Box plot | `sns.boxplot()` | Distribution per group |
| Violin plot | `sns.violinplot()` | Distribution shape per group |
| Strip/swarm plot | `sns.stripplot()` / `sns.swarmplot()` | Individual data points per group |
| Bar plot (mean) | `sns.barplot()` | Mean ± CI per group |
| Scatter plot | `sns.scatterplot()` | Relationship between two variables |
| Regression plot | `sns.lmplot()` | Scatter + regression line per group |
| Heatmap | `sns.heatmap()` | Correlation matrices, expression data |
| Clustermap | `sns.clustermap()` | Hierarchically clustered heatmap |
| Pair plot | `sns.pairplot()` | All pairwise relationships in a dataset |

### When to use seaborn

- You want to compare distributions across groups
- You are working with a pandas DataFrame and want minimal boilerplate
- You need a correlation heatmap or pairplot
- You want built-in confidence intervals on aggregated plots

---

## Plotly

An interactive visualisation library. Charts render as HTML and support hover, zoom, pan, and click events.

**Best for:** Exploratory data analysis, dashboards, interactive presentations.

**Install:** `pip install plotly`

**Official docs:** https://plotly.com/python/

**Plot type gallery:** https://plotly.com/python/basic-charts/

### Plot types (via `plotly.express`)

| Plot | Function | Use case |
|---|---|---|
| Scatter / bubble | `px.scatter()` | Relationships, sized by a third variable |
| Line chart | `px.line()` | Trends over time |
| Bar chart | `px.bar()` | Comparing categories, stacked or grouped |
| Histogram | `px.histogram()` | Distributions |
| Box plot | `px.box()` | Distribution per group |
| Violin plot | `px.violin()` | Distribution shape per group |
| Heatmap | `px.imshow()` | 2D matrix, expression data |
| Choropleth map | `px.choropleth()` | Geographic data |
| Sunburst / treemap | `px.sunburst()` / `px.treemap()` | Hierarchical data |
| Animated charts | `px.scatter(animation_frame=...)` | Data changing over time |

### When to use plotly

- You want to explore data interactively (hover for exact values)
- You are building a web dashboard or Jupyter-based report
- You have a lot of data points and need zoom/pan to explore
- You want animated charts to show change over time

---

## Choosing the Right Library

| Situation | Recommended library |
|---|---|
| Paper / publication figure | matplotlib |
| Distribution or group comparison | seaborn |
| Correlation matrix | seaborn (`heatmap` / `clustermap`) |
| Interactive exploration | plotly |
| Dashboard / web app | plotly |
| Gene expression heatmap | seaborn (`clustermap`) |
| Volcano plot | matplotlib or plotly |
| Quick prototype | seaborn or plotly express |
