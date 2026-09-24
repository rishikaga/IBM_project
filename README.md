# Customer Segmentation, Retention & Revenue Analysis for an Online Retailer

**Author:** Rishika Garg  
**Program:** AICTE | IBM SkillsBuild Data Analytics with AI Internship 2026 — BharatCares

> Full-dataset analysis of customer value, RFM segmentation, retention, revenue drivers, and pre-cutoff lapse prediction.

## Problem Statement

An online retailer wants to know who its valuable customers are, which customers are drifting away, what drives revenue across products, seasons, and countries, and where marketing spend should go. This project segments customers, measures retention, predicts 90-day lapse risk, and recommends targeted marketing actions.

## Key Results

| Result | Computed value |
|---|---:|
| Net revenue | £8,737,227.64 |
| Positive product-sale invoices | 18,402 |
| Customers | 4,334 |
| Average order value | £474.80 |
| Average orders per customer | 4.25 |
| Repeat-customer rate | 65.3% |
| Cancellation invoice rate | 15.5% |
| Cancellation line-item rate | 2.1% |
| Cancelled revenue / gross revenue | 5.1% |
| UK revenue share | 82.9% |
| Month-1 retention (corrected) | 19.7% |
| Month-3 retention (corrected) | 22.9% |
| Top 20% of customers' revenue share | 74.6% |
| Top 10 customers' revenue share | 17.4% |
| Top 50 customers' revenue share | 33.4% |
| Top 20% of products' revenue share | 78.9% |

**Definitions:** Repeat-customer rate is the share of customers with at least two distinct positive-sales invoices. Month-1 retention is the share of eligible acquisition-cohort customers who buy in the next month; month-3 retention uses the third month after acquisition. Corrected figures exclude the left-censored December 2010 cohort and cohorts too recent to observe the relevant month. Uncorrected averages are 18.9% month-1 and 17.9% month-3.

## Segment highlights

| Segment | Customers | Revenue share |
|---|---:|---:|
| Champions | 941 | 64.8% |
| Loyal | 770 | 15.8% |
| Hibernating | 1,077 | 5.9% |
| Can't Lose Them | 179 | 4.9% |
| At Risk | 478 | 4.4% |

## Model versus baselines

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.696 | 0.670 | 0.749 | 0.707 | 0.759 |
| Majority baseline | 0.509 | 0.000 | 0.000 | 0.000 | 0.500 |
| Recency >= 90 days | 0.663 | 0.688 | 0.572 | 0.625 | 0.686 |

Metrics use a held-out test set. Risk tiers are assigned by scoring eligible pre-cutoff customers; the 993 High-risk count is not a test-set count. The recency rule uses >=90 days for threshold metrics and raw recency for ROC-AUC. Logistic Regression adds 0.073 ROC-AUC over continuous recency. The model shows association, not causation.

## Top recommendations

1. Protect the 941 Champions and 770 Loyal customers with priority service and account-based offers.
2. Test a second-purchase offer within 30 days and reminders timed to observed reorder gaps; corrected month-1 retention is 19.7%.
3. Contact the 993 High-risk customers, representing 7.8% of historical revenue, with win-back actions.
4. Manage concentrated overseas wholesale accounts as key accounts; evaluate Germany and France for acquisition.
5. Prepare Q4 campaigns early: November 2011 is the peak month, Q4 contributes 32.9% of complete-month annual revenue, and the peak is 65.8% above average.

## Dataset

Kaggle source: [E-Commerce Data](https://www.kaggle.com/datasets/carrie1/ecommerce-data)  
Original source: [UCI Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail)

The full dataset has 541,909 transaction rows covering December 2010 to December 2011. Download the Kaggle file and save it as `data.csv` beside the notebook. `data.csv` is the only input used by the notebook. Data and generated files are excluded from version control.

## Technologies

Python 3.12, pandas, NumPy, Matplotlib, Seaborn, scikit-learn, Jupyter, nbconvert, ipykernel, openpyxl, and python-docx. Exact versions are pinned in `requirements.txt`.

## Setup and run

```bash
python -m pip install -r requirements.txt
```

If `python` is not on your PATH, use your platform's launcher (`py` on Windows or `python3` on macOS/Linux).

```bash
python -W ignore -m nbconvert --to notebook --execute --inplace RishikaGarg_ConsumerSegmentation.ipynb --ExecutePreprocessor.timeout=1800
```

You can also open `RishikaGarg_ConsumerSegmentation.ipynb` in Jupyter or VS Code and run all cells.

## Project structure

- `RishikaGarg_ConsumerSegmentation.ipynb` — single analysis and model notebook with saved outputs
- `RishikaGarg_ProjectReport.docx` — report with computed tables and embedded figures
- `requirements.txt` — pinned dependencies
- `README.md` — overview and setup instructions
- `cohort_retention_heatmap.png` — cohort retention heatmap
- `country_revenue.png` — revenue by country
- `lapse_confusion_matrix.png` — lapse-model confusion matrix
- `lapse_feature_coefficients.png` — lapse-model feature coefficients
- `lapse_roc_curve.png` — lapse-model ROC curve
- `monthly_revenue_trend.png` — monthly revenue trend
- `segment_revenue_share.png` — segment revenue share
- `top_products.png` — top products

## Charts

![Segment revenue share](segment_revenue_share.png)
![Monthly revenue trend](monthly_revenue_trend.png)
![Lapse-model ROC curve](lapse_roc_curve.png)

The notebook regenerates the charts and JSON outputs; generate_report.py rebuilds the report from them. The dataset is not included and must be downloaded from the link above.
