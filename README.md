# Bitcoin Volatility Forecasting

This repository contains the code, data structure and experimental results associated with a dissertation on Bitcoin volatility forecasting.

The study compares classical time-series models, econometric volatility models, machine learning models and deep learning models under a common forecasting framework.

---

## 1. Project Objective

The main objective of this project is to evaluate the predictive performance of different modelling approaches for Bitcoin volatility forecasting.

The analysis focuses on comparing forecast accuracy across several model families, while also assessing the effect of data transformations on model performance.

The models considered include:

* Naive benchmark;
* Exponential Smoothing State Space models;
* ARIMA models;
* ARCH-family volatility models;
* Support Vector Regression;
* Long Short-Term Memory neural networks.

---

## 2. Dataset

The dataset contains daily Bitcoin closing prices expressed in USD.

From the price series, log-returns are computed and used to construct the volatility proxy:

$$
v_t = r_t^2
$$

where:

$$
r_t = \log(P_t) - \log(P_{t-1})
$$

The squared return series is used as the observed proxy for volatility in the forecasting exercises.

---

## 3. Modelling Framework

The forecasting framework compares models across multiple forecast horizons:

```text
h = 1, 7, 15, 30, 120
```

The following modelling logic is applied:

* ETS, ARIMA, SVR and LSTM models are applied to the volatility proxy based on squared returns;
* ARCH-family models are applied to returns and produce conditional variance forecasts;
* forecasts are evaluated separately for each forecast horizon;
* final performance is summarized using average metrics across horizons.

---

## 4. Data Transformations

The following transformations are considered:

* original volatility proxy;
* logarithmic transformation;
* Yeo-Johnson transformation.

The purpose of these transformations is to assess whether reducing skewness and stabilizing the scale of the volatility proxy improves forecasting accuracy.

---

## 5. Evaluation Metrics

Model performance is evaluated using two complementary metrics:

* Root Mean Squared Error;
* QLIKE loss.

RMSE is used as the main accuracy metric, while QLIKE is included as a complementary loss function commonly used in volatility forecasting.

---

## 6. Repository Structure

```text
Tese_Bitcoin_volatility_clean/
│
├── data/
│   └── raw/
│
├── notebooks/
│
├── results/
│   └── Figures/
│
├── docs/
│
├── src/
│
├── .gitattributes
├── .gitignore
├── requirements.txt
└── README.md
```

---

## 7. Folder Description

### `data/raw`

Contains the original dataset used in the analysis.

### `notebooks`

Contains the Jupyter notebooks used to run the exploratory analysis, model estimation, validation and final comparison.

### `results/Figures`

Contains selected figures generated from the analysis.

### `docs`

Reserved for clean technical documentation related to the modelling framework and repository usage.

### `src`

Reserved for reusable Python modules and functions.

At the current stage, most of the implementation is contained directly in the Jupyter notebooks.

---

## 8. Installation

To install the required Python libraries, run:

```bash
pip install -r requirements.txt
```

A virtual environment is recommended before installing the dependencies.

Example:

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

---

## 9. Main Results

The empirical results suggest that more complex models do not automatically guarantee better volatility forecasts.

In the final comparison, SVR achieved the best average RMSE among the evaluated model families, while LSTM became competitive after transformation of the volatility proxy. Classical models such as ETS and ARIMA also achieved stable results, especially when transformations were applied.

ARCH-family models require a specific interpretation, since they are fitted to returns and produce conditional variance forecasts rather than direct forecasts of the squared-return proxy.

Overall, the results highlight the importance of preprocessing, transformation choice and consistent evaluation when comparing volatility forecasting models.

---

## 10. Notes

This repository is intended as a clean and shareable version of the project.

Large intermediate files, cached model outputs, trained models and personal thesis documents are not included in this repository.
