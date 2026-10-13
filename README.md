# Customer Churn Prediction Project

End-to-end churn analytics project: a scikit-learn model that ranks bank customers by churn risk,
a Streamlit scoring app, and a Power BI report on a relational bank data model.

- Project page: <https://ldongmon.github.io/>
- Streamlit app: <https://churnprobaapps-ftuk5k4wd7umfmm5angxsk.streamlit.app/> (source: [churn_proba_apps](https://github.com/ldongmon/churn_proba_apps))

## Results

Model trained on the public, anonymised *Bank Customer Churn* dataset (Kaggle): 10,000 customers, 20.4% churners.
Stratified 80/20 split; figures below are measured on the 2,000-customer test set (408 churners).

| Metric | Logistic Regression | Random Forest (selected) |
|---|---|---|
| Accuracy | 0.813 | 0.869 |
| Precision (churn) | 0.62 | 0.80 |
| Recall (churn) | 0.21 | 0.47 |
| F1 (churn) | 0.32 | 0.59 |
| ROC-AUC | 0.778 | 0.867 |

Always predicting "no churn" would already give 79.6% accuracy, so the model is judged on the churn class:
it is right four times out of five when it flags a customer, and it finds about half of the customers who leave.
The `Complain` column (r = 0.996 with the target) is removed as a leakage variable, together with the identifier
columns. The probabilities are not calibrated: they rank customers, they are not a literal chance of leaving.

Risk bands (single definition, cut-offs 0.20 / 0.40 / 0.70): Low 62.4%, Moderate 20.2%, High 11.1%, Critical 6.2%
of the test customers.

## Repository content

| File | Content |
|---|---|
| `index.html` | Project page (GitHub Pages) |
| `CHURN MODELING_REPORT.ipynb` | Modelling notebook, executed end to end |
| `CHURN MODELING_REPORT.qmd` / `.html` / `CHURN-MODELING_REPORT.pdf` | Quarto source and rendered reports |
| `Customer-Churn-Records.csv` | Training data (Kaggle Bank Customer Churn) |
| `churn_model.pkl` | Saved Random Forest pipeline (scikit-learn 1.6.1) |
| `customer_churn_predictions.csv` | Scores and risk bands of the 2,000 test customers |
| `MY_Dashboard.pbix` | Power BI report (one page) |
| `customers.csv`, `accounts.csv`, `transactions.csv`, `products.csv` | Synthetic tables behind the Power BI model (200 customers, 407 accounts, 8,758 transactions, 309 product holdings) |
| `DOCUMENTATION.pdf` | Technical documentation: model, data model, measures, limitations |
| `powerbi-dashboard-preview.png` | Screenshot of the report ("High Value" segment selected) |

## Important note on the dashboard data

The four Power BI tables are synthetic. The churn score shown in the dashboard is a simulated column of the
synthetic customer table; it is not an output of the model above. The dashboard shows how a churn score is
consumed in a BI layer. See `DOCUMENTATION.pdf`, section 2.2.

## Reproduce

```bash
pip install scikit-learn==1.6.1 pandas matplotlib openpyxl jupyter
jupyter nbconvert --to notebook --execute --inplace "CHURN MODELING_REPORT.ipynb"
```

Running the notebook regenerates `churn_model.pkl` and the prediction files.

## Contact

Leprince Dongmo Nanda · <leprince.dongmo@yahoo.fr> · [LinkedIn](https://www.linkedin.com/in/leprince-dongmo-nanda/)
