# Project 01 — Air Quality Analytics and Insight Report

**Intern:** Darshan Suresh S
**Level:** Beginner to Intermediate | **Tools:** Python, Pandas, NumPy, Matplotlib, Jupyter

## Problem

Urban air-quality sensor data is noisy, incomplete, and hard to interpret directly. This project turns raw
hourly sensor readings into a clean analytical dataset and produces evidence-based insights about pollution
patterns, environmental conditions, and data quality.

## Dataset

- **Source:** UCI Machine Learning Repository — [Air Quality Data Set](https://archive.ics.uci.edu/dataset/360/air+quality)
- **Size:** 9,358 hourly records (9,357 real rows after removing trailing empty rows/columns), March 2004 – February 2005, an Italian city
- **Missing-value marker:** `-200`
- Download `AirQualityUCI.csv` from the link above and place it at `data/AirQualityUCI.csv`.

## Approach

1. **Load & audit** — parsed the semicolon-delimited, decimal-comma source file; checked shape, dtypes, duplicates.
2. **Datetime features** — combined Date + Time into a datetime index; derived hour, day, month, weekday, is_weekend.
3. **Missing-value treatment** — replaced -200 with NaN; dropped NMHC_GT (~90% missing); time interpolation (6h limit) + hour-of-day median fallback for the rest.
4. **NumPy statistics** — mean/median/std/percentiles/IQR outlier bounds, plus two custom metrics: a Pollution Index and a Sensor Reliability Ratio.
5. **Pandas aggregations** — groupby, pivot_table, resample, and corr across hour/day/month/weekend splits.
6. **Visualizations** — 8 Matplotlib charts.
7. **Insights & limitations** — documented in the notebook and PDF report.
8. **Export** — cleaned_air_quality.csv and summary_statistics.csv.

## Repository Structure

\`\`\`
air-quality-analytics/
|-- data/                      # raw + cleaned data, summary stats
|-- notebooks/
|   `-- 01_air_quality_analysis.ipynb
|-- assets/                    # exported PNG charts
|-- reports/
|   `-- Project_01_Report.pdf
`-- README.md
\`\`\`

## How to Run

\`\`\`bash
python -m venv venv
venv\\Scripts\\activate      # Windows
pip install -r requirements.txt
jupyter notebook notebooks/01_air_quality_analysis.ipynb
# Kernel > Restart & Run All
\`\`\`

## Key Findings (Summary)

- Pollution (CO, NOx) shows a clear weekday rush-hour double peak (~08:00 and ~18:00-20:00).
- Winter months show higher CO than summer months.
- The low-cost metal-oxide CO sensor correlates strongly (r ≈ 0.82) with the certified analyzer.
- NMHC_GT is unusable for analysis (~90% missing) and was excluded — a documented dataset limitation.

## Dataset Citation

De Vito, S. (2016). Air Quality [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C59K5F