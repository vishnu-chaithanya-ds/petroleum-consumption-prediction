# ⛽ Petroleum Product Consumption Prediction

Predicting monthly consumption of 12 petroleum products (HSD, MS, LPG, ATF and more) from historical data with a Random Forest regressor.

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)

## Problem
Energy planners and petroleum companies need to estimate fuel demand to plan production and supply. This project predicts monthly consumption (in thousand metric tonnes) for each product from the month, year and product type.

## Dataset
- 492 rows × 5 columns: `Month`, `Year`, `PRODUCTS`, `Quantity (000 Metric Tonnes)`, `updated_date`
- 12 products: ATF, Bitumen, FO & LSHS, HSD, LDO, LPG, Lubricants & Greases, MS, Naphtha, Others, Petroleum coke, SKO
- Coverage: January 2020 to August 2023, no missing values
- `updated_date` was dropped because it carries no information about consumption

## Method
1. Rename columns and validate values
2. EDA: average monthly consumption per year, total consumption per product, boxplots by product
3. Label-encode `Month` and `Products`, remove outliers with the IQR rule
4. 80/20 train–test split
5. `RandomForestRegressor` (random_state = 1, n_estimators = 5) and feature-importance plot

## Results
| Metric | Value |
|---|---|
| R² (test) | **0.913** |
| R² (train) | 0.975 |

**Findings:** HSD (diesel) has the highest total consumption (272,769 thousand tonnes over the period), and average monthly consumption rises year over year from 2020.

## Limitations and next steps
- Report MAE, RMSE and MAPE next to R², and compare with a simple baseline (for example each product's average).
- Use a **time-based split** (train on 2020–2022, test on 2023) if the goal is forecasting; a random split mixes past and future months.
- The IQR outlier rule is applied to all products together, so it can remove legitimate high-volume rows (such as HSD). Apply it per product or use a log transform, and report how many rows were removed.
- Encode `Month` as 1–12 instead of alphabetical labels, and increase `n_estimators` (the default is 100).
- Compare Linear Regression, Gradient Boosting and tuned Random Forest with cross-validation and `GridSearchCV`.
- 2020 includes the COVID-19 period, which affects the trend.

## Run it
```bash
git clone https://github.com/vishnu-chaithanya-ds/petroleum-consumption-prediction.git
cd petroleum-consumption-prediction
pip install -r requirements.txt
# add data/petrol_consumption.csv (see data/README.md)
jupyter notebook notebooks/petroleum_consumption_prediction.ipynb
```

## Author
**Tadipatri Vishnu Chaithanya** · [Portfolio](https://vishnuchaithanya.netlify.app/) · [LinkedIn](https://www.linkedin.com/in/tadipatri-vishnu-chaithanya-52817037b) · [GitHub](https://github.com/vishnu-chaithanya-ds)
