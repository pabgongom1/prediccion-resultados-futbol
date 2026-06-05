# Statistical Methods for Football Outcome Prediction

[Versión en español](README.es.md)

Bachelor's Thesis — Double Degree in Mathematics and Statistics, University of Seville (2024–2025).

This project explores a range of statistical and machine learning techniques to predict football match outcomes in the Spanish first division (LaLiga), and evaluates the predictions through a betting-based framework used as a real-world measure of whether the models capture genuine predictive value.

## Overview

Two prediction targets are addressed:

* **Number of goals** per team, used to bet on the Over/Under 2.5 goals market.
* **Match result (1X2)** — home win, draw, or away win — used to bet directly on the outcome.

Models are trained on LaLiga seasons 2018/19–2022/23 and evaluated on the 2023/24 season. Predictions are compared against Bet365 odds, and performance is measured primarily by **Return on Investment (ROI)**, which reflects whether the models would have been profitable rather than just accurate.

## Models

|#|Model|Type|Target|
|-|-|-|-|
|1|Poisson with independence|Classical|Goals|
|2|Poisson with independence + time weighting|Classical|Goals|
|3|Bivariate Poisson + time weighting|Classical|Goals|
|4|Random Forest (regression)|Machine learning|Goals|
|5|Random Forest (classification)|Machine learning|Result (1X2)|
|6|XGBoost (classification)|Machine learning|Result (1X2)|

The goals-based models (1–4) build on the classical Maher (1982) and Dixon–Coles (1997) frameworks, including a bivariate extension that captures correlation between the two teams' scores. The result-based models (5–6) use team-level covariates (previous-season standings, squad market value, average age, summer transfer spend, and dynamic ELO ratings).

## Key results

**Goals models — Over/Under 2.5 market:**

|Model|Bets|ROI|
|-|-|-|
|Poisson independence|37|10.4%|
|Poisson + time weighting|71|19.1%|
|**Bivariate Poisson**|38|**23.6%**|
|Random Forest|19|11.3%|

**Result models — 1X2 market (mean ROI over 100 trained models):**

|Model|Global accuracy|ROI|
|-|-|-|
|Random Forest|48.6%|5.3%|
|**XGBoost**|**51.5%**|**9.1%**|

Two findings stand out. Among the goals models, the **bivariate Poisson with time weighting achieved the best return (23.6% ROI)**, showing that modeling the dependence between teams' scores and weighting recent matches both add real value. Among the result models, **XGBoost outperformed Random Forest** in both accuracy and ROI, and was notably stronger at predicting away wins — the hardest class to call and the one tied to the highest odds. Every regression model produced a positive net return over the season.

## Repository structure

```
.
├── README.md          # This file (English)
├── README.es.md       # Spanish version
├── src/               # R Markdown source files (models and analysis)
├── data/              # Match results and team-level datasets (CSV)
└── docs/              # Full thesis (PDF) and defense slides
```

## Tech stack

R, with `caret`, `randomForest`, `xgboost`, `dplyr`, `ggplot2`, `readr`, `readxl` and `kableExtra`.

## Data sources

* [Football-Data.co.uk](https://www.football-data.co.uk/spainm.php) — historical match results and Bet365 odds.
* [Transfermarkt](https://www.transfermarkt.es) — squad market values, average age and transfer spend.
* [ClubElo](http://clubelo.com/) via the [xgabora/Club-Football-Match-Data-2000-2025](https://github.com/xgabora/Club-Football-Match-Data-2000-2025) repository — ELO ratings.

## Limitations \& future work

The classification betting strategy does not incorporate the bookmaker's implied probabilities (unlike the goals strategy), which limits the detection of positive expected-value bets. Only Bet365 odds were used; adding more bookmakers would help surface better value opportunities. A natural next step is to apply the models to further seasons to test whether their performance holds over time.

## Author

Pablo González Gómez — [LinkedIn](https://www.linkedin.com/in/pablo-gonzalez-gomez)


