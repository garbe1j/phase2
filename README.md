# Phase 2 (Silver) – Data Wrangling: IRCC/CIC Application Processing Times

**Status: submission complete.** All required sections (1–8) are in `phase2.ipynb`, and every cell has been run with its output saved.

## Files submitted
| File | Purpose |
|------|---------|
| `phase2.ipynb` | Main deliverable: title, data acquisition, initial exploration, cleaning, enrichment, validation checks, final dataset, references. |
| `README.md` | This file. |

## Required: download the dataset before running
The raw data file is **not included** in this submission. To re-run the notebook:

1. Download `processed_cic_data.csv` from Kaggle: https://www.kaggle.com/datasets/ayraza/canada-visa-processing-time-last-updated-july-23?select=processed_cic_data.csv (dataset "Canada Visa Processing Time (last updated July 23)" by *ayraza*).
2. Save it in the **same folder** as `phase2.ipynb`, keeping the filename `processed_cic_data.csv`.
3. Run all cells (Python 3 with `pandas`, `numpy`, `matplotlib`).

Running the notebook creates four output files in that folder (not submitted): `cic_processing_times_clean.csv`, `cic_private_refugee_times_clean.csv`, `cic_monthly_trend.csv`, `cic_country_summary.csv`.

## Summary of what was done
- Removed ~43.7k duplicate rows (repeat scrapes on the same date), resolving 45 conflicting pairs by keeping the populated value.
- Fixed country names (HTML symbols removed; Swaziland → Eswatini, Turkey → Türkiye): 212 → 210 countries.
- Parsed dates; converted free-text times (`12 weeks`, `173 days`, `3 months`) to numbers and normalized to days (month = 30.4375 days).
- Replaced the `Not enough data` placeholder and blanks with an explicit `status` column; nothing was imputed.
- Split the private-sponsorship program (sponsor/refugee times, assumed to be months) into its own table.
- Added date fields, wait categories, rolling averages, change vs. previous snapshot, comparisons to the median and each country's average, one merge, and two aggregations.
- 16 validation checks, all passing.

## Notes / assumptions
- `sponsor_time` and `refugee_time` have no unit in the source; they are treated as months.
- `Macedonia` keeps IRCC's label.

