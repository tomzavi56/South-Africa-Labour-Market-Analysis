# South African Labour Market Analysis

## Overview

This project analyses South Africa's labour market with a focus on unemployment. It combines national quarterly unemployment trends from 2008 to 2026 Q2 with Statistics South Africa (Stats SA) Quarterly Labour Force Survey (QLFS) microdata for 2026 Q2.

The project covers data cleaning, exploratory data analysis, provincial and demographic comparisons, hypothesis testing, logistic regression, and time-series forecasting.

## Research Questions

The analysis addresses the following questions:

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

The cleaned national time-series dataset used in the repository is:

- `south_africa_unemployment_2008_2026.csv`

Survey weights are used for the provincial and demographic unemployment-rate estimates.

## Key Findings

### National unemployment trend

- The national quarterly unemployment series contains **74 observations** from 2008 Q1 to 2026 Q2.
- The average unemployment rate over the period is approximately **27.94%**.
- The lowest observed rate is **21.5% in 2008 Q4**.
- The highest observed rate is **35.3% in 2021 Q4**.
- The long-run pattern shows a substantial increase in unemployment, particularly from the late 2010s into the early 2020s.
- The largest quarter-to-quarter movements occurred around the COVID-19 period, which should be interpreted cautiously because labour-force participation and unemployment measurement were unusually affected.

### Provincial differences — Q2 2026

Weighted unemployment estimates show substantial variation across provinces.

- **Eastern Cape:** approximately **47.5%**
- **North West:** approximately **38.1%**
- **Free State:** approximately **37.3%**
- **Mpumalanga:** approximately **36.6%**
- **Gauteng:** approximately **34.6%**
- **KwaZulu-Natal:** approximately **32.5%**
- **Limpopo:** approximately **32.0%**
- **Northern Cape:** approximately **28.7%**
- **Western Cape:** approximately **19.5%**

Eastern Cape records the highest estimated unemployment rate, while Western Cape records the lowest.

### Gender differences — Q2 2026

Weighted unemployment is higher among women than men.

- **Female:** approximately **37.4%**
- **Male:** approximately **30.3%**

### Age differences — Q2 2026

Unemployment is most severe among younger people and generally declines with age.

Approximate rates include:

- Ages 15–19: **77%**
- Ages 20–24: **61%**
- Ages 25–29: **45%**

The weighted **NEET rate for youth aged 15–34 is 45.38%**.

### Education

People with tertiary education have the lowest unemployment rate among the education groups analysed. The descriptive results indicate a strong association between educational attainment and labour-market outcomes, although the analysis does not establish causality.

## Hypothesis Testing

Two chi-square tests of independence were carried out using sample counts.

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

Selected results from the model include:

- **Male odds ratio: 0.650** — males have lower estimated odds of unemployment than females, holding the other variables constant.
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

## Repository Structure

| File | Purpose |
|---|---|
| `01_data_loading_and_exploration.ipynb` | Initial data loading and exploration |
| `02_data_cleaning_and_validation.ipynb` | Cleaning and validating the national unemployment series |
| `03_exploratory_data_analysis.ipynb` | Descriptive statistics, trends and visualisations |
| `04_provincial_and_demographic_analysis.ipynb` | Province, gender, age, education and youth analysis |
| `05_hypothesis_testing.ipynb` | Chi-square tests of labour-market differences |
| `06_regression_analysis.ipynb` | Logistic regression of unemployment status |
| `07_time_series_forecasting.ipynb` | Stationarity testing, ARIMA, ETS and forecasting |
| `south_africa_unemployment_2008_2026.csv` | Cleaned national quarterly unemployment dataset |

## Tools and Methods

- Python
- Google Colab
- Pandas
- NumPy
- Matplotlib
- SciPy
- Statsmodels
- Scikit-learn
- Exploratory Data Analysis
- Descriptive Statistics
- Weighted survey estimates
- Chi-square tests
- Logistic regression
- Augmented Dickey-Fuller testing
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

The repository is now being refined for portfolio presentation and documentation.

## Author

**Tom Ntaba**

Aspiring Statistical / Data Analyst
