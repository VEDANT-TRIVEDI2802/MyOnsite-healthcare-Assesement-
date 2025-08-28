# Simple AI Assessment: Product Review Analyzer & Comparator

This is a lightweight AI project that analyzes product reviews for sentiment, compares products by a weighted score (price, rating, sentiment), and generates a visual + CSV report.

## Features
- Parses a small sample dataset (`data/products.json`).
- Simple lexicon-based sentiment analyzer (no downloads required).
- Weighted ranking: lower price, higher rating, and positive sentiment score boost a product's final score.
- Generates a bar chart and CSV in `reports/`.

## Project Structure
```text
simple_ai_assessment/
├─ data/
│  ├─ products.json
│  └─ reviews.csv
├─ reports/                   # outputs are written here
├─ src/
│  ├─ main.py                 # entry point (CLI)
│  ├─ sentiment.py            # tiny sentiment engine
│  ├─ data_loader.py          # read JSON/CSV
│  ├─ compare.py              # ranking logic
│  └─ report.py               # charts + CSV/markdown report
├─ requirements.txt
└─ README.md
```

## Quickstart

```bash
# (Optional) create a virtual environment
python -m venv .venv
. .venv/bin/activate   # Windows: .venv\Scripts\activate

pip install -r requirements.txt

# Run the analyzer
python src/main.py --make-report

# Outputs:
# - reports/summary.csv
# - reports/score_bar_chart.png
# - reports/report.md
```

## How it works
1. Loads products and their reviews from `data/products.json`.
2. Uses a small positive/negative lexicon to compute a compound sentiment score per review and averages by product.
3. Normalizes price (lower is better) and rating (0–1), then combines with sentiment into a final score:
   ```
   final_score = 0.5 * sentiment + 0.3 * rating_norm + 0.2 * price_norm_inverse
   ```
4. Produces a sortable CSV and a bar chart.

## Customize
- Add your own products/reviews in `data/products.json`.
- Adjust weights in `src/compare.py`.
- Replace the lexicon in `src/sentiment.py` with a bigger one if desired.
