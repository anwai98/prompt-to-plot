# Using Your Own Data

The notebook works with any pandas DataFrame. Here is how to load your own CSV and start prompting.

## Loading a CSV in Colab

**Option 1 — Upload a file from your computer:**

```python
from google.colab import files
uploaded = files.upload()  # opens a file picker

import pandas as pd
import io
df = pd.read_csv(io.BytesIO(list(uploaded.values())[0]))
df.head()
```

**Option 2 — Load from Google Drive:**

```python
from google.colab import drive
drive.mount('/content/drive')

import pandas as pd
df = pd.read_csv('/content/drive/MyDrive/your_file.csv')
df.head()
```

**Option 3 — Load from a public URL:**

```python
import pandas as pd
df = pd.read_csv('https://example.com/your_file.csv')
df.head()
```

---

## Prompting with Your Own Data

Once your DataFrame is loaded, pass it directly to `ask_gemini_to_plot`:

```python
ask_gemini_to_plot(
    df=df,
    df_name='df',
    user_request='Describe the plot you want here.',
    library_hint='seaborn',
)
```

The function automatically sends the column names, types, and first 3 rows to Gemini, so it understands your data without you having to explain the structure.

---

## Tips for Custom Data

- **Check column names first** — run `df.columns.tolist()` and use the exact names in your prompts.
- **Check data types** — run `df.dtypes` to confirm which columns are numeric vs categorical.
- **Handle missing values** — if your data has NaNs, add "ignore missing values" to your prompt, or clean the data first with `df.dropna()`.
- **Large datasets** — the notebook sends only 3 sample rows to Gemini, so large files are fine. For faster plots, consider passing a sample: `df.sample(1000)`.
