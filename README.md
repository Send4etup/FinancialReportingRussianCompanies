# Financial Reporting of Russian Companies

Exploratory data analysis of Russian companies using the [RFSD dataset](https://huggingface.co/datasets/irlspbru/RFSD) — annual unconsolidated financial statements of Russian firms (2011–2024).

## What's inside

**`main.ipynb`** — single analysis notebook covering:

1. **Distribution analysis** — histograms for `age` (company age), `okopf` (legal form classifier, ОКОПФ), `okfc` (ownership form classifier, ОКФС). All three show right-skewed distributions with outliers at high values.

2. **Scatter plots** — pairwise relationships between `age`, `okopf`, and `totals_adjustment` with Pearson correlation coefficients.

3. **Correlation heatmap** — full correlation matrix across 20 numeric columns (seaborn heatmap).

4. **Balance sheet correlation deep-dive** — scatter plots for the most correlated pairs:
   - `line_1100` (Non-current assets total) ↔ `line_1150`, `line_1160`, `line_1170`, `line_1180`
   - `line_1160`, `line_1170` ↔ `line_1200`, `line_1210`, `line_1220`

## Dataset

| Field | Value |
|---|---|
| Source | Hugging Face — [`irlspbru/RFSD`](https://huggingface.co/datasets/irlspbru/RFSD) |
| Coverage | 2011–2024, annual, unconsolidated |
| Format | CSV (exported subset) |

Column naming follows Russian balance sheet line codes (строки бухгалтерского баланса): `line_1100` = total non-current assets, `line_1150` = fixed assets, `line_1200` = total current assets, etc.

## Stack

- Python 3.x
- pandas
- matplotlib
- seaborn

## Setup

```bash
git clone https://github.com/Send4etup/FinancialReportingRussianCompanies.git
cd FinancialReportingRussianCompanies
pip install pandas matplotlib seaborn
jupyter notebook main.ipynb
```

Place the dataset CSV as `file.csv` in the root directory before running.

## Key findings

- `line_1100` strongly correlates with `line_1150`, `line_1160`, `line_1170`, `line_1180`, `line_1190` — expected, since it's the sum of non-current asset sub-items.
- `line_1160` and `line_1170` correlate with `line_1200`, `line_1210`, `line_1220` — cross-section correlation between financial investments and current asset items.
- `okopf` and `okfc` contain classifier codes; their distributions reflect the legal and ownership structure makeup of Russian companies.
- Some balance sheet columns (`line_*`) have significant missing values — likely reported only under specific accounting standards or company types.
