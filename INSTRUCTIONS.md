# How to Run This Notebook

Follow these 3 steps. The whole setup takes about 2 minutes.

---

## Step 1 — Get a free Gemini API key

1. Go to [Google AI Studio](https://aistudio.google.com/app/apikey) (sign in with your Google account)
2. Click **"Create API key"**
3. Copy the key — you'll need it in Step 2

![Get API key from Google AI Studio](screenshots/01_aistudio_create_key.png)

---

## Step 2 — Add the key to Colab Secrets

1. Open the notebook in Colab using the button in the README
2. In the left sidebar, click the **🔑 key icon** to open Secrets
3. Click **"Add new secret"**
4. Set the name to exactly `GEMINI_API_KEY` and paste your key as the value
5. Toggle **"Notebook access"** on

![Add secret in Colab](screenshots/02_colab_add_secret.png)

> You only need to do Steps 1 and 2 once. The key is saved to your Colab account.

---

## Step 3 — Run the notebook

1. In the top menu, click **Runtime → Run all**
2. The first cell will install dependencies — this takes about 10 seconds
3. Each example cell will call Gemini, print the generated code, and display the plot

![Run all cells](screenshots/03_colab_run_all.png)

---

## Trying your own prompts

Scroll to **Section 8 — Your Turn!** at the bottom of the notebook.

Edit the three variables in the cell:
- `MY_DATASET` — which dataset to use
- `MY_LIBRARY` — `'matplotlib'`, `'seaborn'`, or `'plotly'`
- `MY_REQUEST` — your plain-English description of the plot

Then run that cell.

![Free-form prompt cell](screenshots/04_your_turn_cell.png)

---

## Troubleshooting

| Problem | Fix |
|---|---|
| `UserDataError: Secret not found` | Make sure the secret name is exactly `GEMINI_API_KEY` (case-sensitive) and "Notebook access" is toggled on |
| `ResourceExhausted` error | You've hit the rate limit (15 requests/min). Wait a moment and re-run |
| Plot doesn't appear | Re-run the cell — Gemini occasionally generates slightly broken code; a second attempt usually fixes it |
