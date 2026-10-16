# South African Labour Market Analysis

## Overview

This project analyses South Africa's labour market with a focus on unemployment. It combines national quarterly unemployment trends from 2008 to 2026 Q2 with Statistics South Africa (Stats SA) Quarterly Labour Force Survey (QLFS) microdata for 2026 Q2.

The project covers data cleaning, exploratory data analysis, provincial and demographic comparisons, hypothesis testing, logistic regression, and time-series forecasting.

## Research Questions

1. How has South Africa's unemployment rate changed over time?
2. Which provinces have the highest and lowest unemployment rates?
3. How does unemployment differ by gender, age and education?
4. How severe is youth labour-market exclusion?
5. Are employment status and demographic/geographic characteristics statistically associated?
6. Which factors are associated with the probability of unemployment?
7. Is the national unemployment series stationary?
8. Which forecasting approach performs better between selected ARIMA and ETS models?
9. What does the selected model suggest about unemployment over the next several quarters?

## Data

The project uses official Statistics South Africa (Stats SA) Quarterly Labour Force Survey data.

Two main sources are used:

- **QLFS Trends 2008–2026 Q2** for the national quarterly unemployment time series.
- **QLFS 2026 Q2 unit-record data** for provincial and demographic analysis.

The cleaned national time-series dataset is stored in:

`data/south_africa_unemployment_2008_2026.csv`

Survey weights are used for the provincial and demographic unemployment-rate estimates.

## Key Findings

### National unemployment trend

The national series contains **74 quarterly observations** from 2008 Q1 to 2026 Q2. The average unemployment rate is approximately **27.94%**, with a low of **21.5% in 2008 Q4** and a high of **35.3% in 2021 Q4**.

![South African unemployment rate and long-term trend](visuals/unemployment_long_term_trend.png)

The long-run pattern shows a substantial rise in unemployment, particularly from the late 2010s into the early 2020s. The largest quarter-to-quarter movements occurred around the COVID-19 period and should be interpreted cautiously.

### Provincial differences — Q2 2026

Weighted unemployment estimates vary substantially across provinces. Eastern Cape records the highest estimated rate at approximately **47.5%**, while Western Cape records the lowest at approximately **19.5%**.

![Unemployment rate by province](visuals/unemployment_by_province.png)

### Gender differences — Q2 2026

Weighted unemployment is higher among women than men:

- **Female:** approximately **37.4%**
- **Male:** approximately **30.3%**

![Unemployment rate by gender](visuals/unemployment_by_gender.png)

### Age differences — Q2 2026

Unemployment is most severe among younger people and generally declines with age. Approximate rates include **77% for ages 15–19**, **61% for ages 20–24**, and **45% for ages 25–29**.

The weighted **NEET rate for youth aged 15–34 is 45.38%**.

![Unemployment rate by age group](visuals/unemployment_by_age.png)

### Education

People with tertiary education have the lowest unemployment rate among the education groups analysed. The results show a clear association between education level and labour-market outcomes, although the analysis does not establish causality.

![Unemployment rate by education level](visuals/unemployment_by_education.png)

## Hypothesis Testing

Two chi-square tests of independence were conducted using raw sample counts.

### Gender and employment status

- Chi-square statistic: **105.569**
- Degrees of freedom: **1**
- p-value: **< 0.001**

The null hypothesis of independence is rejected, indicating a statistically significant association between gender and employment status in the sample.

### Province and employment status

- Chi-square statistic: **425.994**
- Degrees of freedom: **8**
- p-value: **< 0.001**

The null hypothesis is rejected, indicating a statistically significant association between province and employment status in the sample.

## Logistic Regression

A logistic regression model was fitted with unemployment status as the binary outcome and gender, age, education and province as predictors.

Selected results:

- **Male odds ratio: 0.650** — lower estimated odds of unemployment than females, holding other variables constant.
- **Age odds ratio: 0.936** — each additional year of age is associated with lower estimated odds of unemployment.
- **Tertiary education odds ratio: 0.349** relative to the reference education category.
- **Western Cape odds ratio: 0.302** relative to Eastern Cape.

The overall model is statistically significant.

## Time-Series Forecasting

The Augmented Dickey-Fuller test indicates that the unemployment series is non-stationary in levels:

- ADF statistic: **-0.9637**
- p-value: **0.7663**

After first differencing, the series becomes stationary:

- ADF statistic: **-8.1253**
- p-value: **< 0.001**

Several ARIMA specifications and ETS models were evaluated using the final eight quarters as a test set.

### Best ARIMA model

**ARIMA(0,1,1)**

- MAE: **0.804**
- RMSE: **0.973**

### Best ETS model

**ETS — Level only**

- MAE: **0.800**
- RMSE: **0.968**

The ETS level-only model marginally outperformed ARIMA(0,1,1) on the holdout sample. Its eight-quarter forecast suggests unemployment remaining broadly stable at around **33%**, rather than showing a strong upward or downward movement.

![South African unemployment rate forecast](visuals/unemployment_forecast.png)

## Repository Structure

```text
South-Africa-Labour-Market-Analysis/
│
├── README.md
├── .gitignore
│
├── data/
│   └── south_africa_unemployment_2008_2026.csv
│
├── notebooks/
│   ├── 01_data_loading_and_exploration.ipynb
│   ├── 02_data_cleaning_and_validation.ipynb
│   ├── 03_exploratory_data_analysis.ipynb
│   ├── 04_provincial_and_demographic_analysis.ipynb
│   ├── 05_hypothesis_testing.ipynb
│   ├── 06_regression_analysis.ipynb
│   └── 07_time_series_forecasting.ipynb
│
└── visuals/
    ├── unemployment_long_term_trend.png
    ├── unemployment_by_province.png
    ├── unemployment_by_gender.png
    ├── unemployment_by_age.png
    ├── unemployment_by_education.png
    └── unemployment_forecast.png
```

## Notebook Guide

| Notebook | Purpose |
|---|---|
| [01 — Data Loading and Exploration](notebooks/01_data_loading_and_exploration.ipynb) | Loading and initially exploring the labour-market data |
| [02 — Data Cleaning and Validation](notebooks/02_data_cleaning_and_validation.ipynb) | Cleaning and validating the national unemployment series |
| [03 — Exploratory Data Analysis](notebooks/03_exploratory_data_analysis.ipynb) | Descriptive statistics, trends and visualisations |
| [04 — Provincial and Demographic Analysis](notebooks/04_provincial_and_demographic_analysis.ipynb) | Province, gender, age, education and youth analysis |
| [05 — Hypothesis Testing](notebooks/05_hypothesis_testing.ipynb) | Chi-square tests of labour-market differences |
| [06 — Regression Analysis](notebooks/06_regression_analysis.ipynb) | Logistic regression of unemployment status |
| [07 — Time-Series Forecasting](notebooks/07_time_series_forecasting.ipynb) | Stationarity testing, ARIMA, ETS and forecasting |

## Tools and Methods

Python, Google Colab, Pandas, NumPy, Matplotlib, SciPy, Statsmodels and Scikit-learn were used for:

- Exploratory data analysis and descriptive statistics
- Weighted survey estimates
- Chi-square hypothesis tests
- Logistic regression
- Augmented Dickey-Fuller stationarity testing
- ARIMA forecasting
- Exponential Smoothing / ETS
- MAE and RMSE forecast evaluation

## Limitations

The QLFS is based on a complex survey design. Survey weights were used when calculating provincial and demographic unemployment-rate estimates.

The chi-square tests use raw sample counts and should therefore be interpreted as simplified inferential analyses rather than fully survey-design-adjusted tests. The logistic regression is also exploratory and does not fully account for the QLFS complex survey design.

The forecasting exercise is based on a relatively short quarterly series and evaluates a limited set of ARIMA and ETS specifications. Forecasts should therefore be interpreted as statistical projections rather than certain future outcomes.

## Data Source

Statistics South Africa (Stats SA), **Quarterly Labour Force Survey (QLFS)**.

The analysis and interpretation in this repository are independently produced from Stats SA data.

## Project Status

✅ Core statistical analysis completed.

## Author

**Tom Ntaba**

Aspiring Statistical / Data Analyst
