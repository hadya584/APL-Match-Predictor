# ⚽ APL Match Predictor

A machine learning model that predicts whether a team will win an APL soccer match, using a Random Forest classifier trained on two seasons of match results.

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?logo=scikitlearn&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white)

## Overview

The dataset (`matches.csv`) has **299 match results** from September 2022 to December 2024 across **19 teams**. Each row records the team, date, kickoff time, venue, opponent, result, and goals for and against.

The notebook cleans the data, engineers numeric features, and trains a model to answer one question: **will this team win?**

## How It Works

1. **Clean**: parse match dates into datetime objects.
2. **Engineer features**:
   - `venue_code`: home or away, encoded as a category
   - `opp_code`: the opponent, encoded as a category
   - `hour`: kickoff hour, taken from the match time
   - `day_code`: day of the week
3. **Set the target**: `1` for a win, `0` for a loss or draw.
4. **Train and test by time**: the model trains on 2022 matches and tests on 2023 onward, so it never sees the future while learning.
5. **Model**: `RandomForestClassifier(n_estimators=50, min_samples_split=10)`.
6. **Evaluate**: accuracy, precision, and a confusion matrix.

## Results

| Metric | Score |
| --- | --- |
| Accuracy | 52.8% |
| Precision (predicting wins) | 43.4% |
| Baseline (always predict "no win") | 57.8% |

This first model **does not beat the simple baseline**, which shows that venue, opponent, and schedule alone aren't enough to predict a result. Recent team form is the missing signal, which leads to the next steps below.

## Next Steps

- Add **rolling averages** of each team's recent performance (goals for and against over the last 3–5 matches)
- Combine each match's two team perspectives into one prediction
- Tune hyperparameters and compare against logistic regression and gradient boosting

## Run It

```bash
git clone https://github.com/hadya584/APL-Match-Predictor.git
cd APL-Match-Predictor
pip install pandas scikit-learn jupyter
jupyter notebook Match-Predictor.ipynb
```
