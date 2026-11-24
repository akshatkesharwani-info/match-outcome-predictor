# Football Match Outcome Predictor

Predict home win, draw or away win for international football matches using Elo ratings and recent form.

## STAR
- **Situation:** Football results are noisy and draws are hard to call, so a model has to be compared with simple rules to know if it adds anything.
- **Task:** Predict match outcomes using only information available before kick-off and test on the newest matches.
- **Action:** Loaded 50,099 international results (data up to 17 Nov 2026). Went through matches in date order and built Elo ratings (with home advantage and goal difference), last 5 match form and a neutral venue flag for each team before each match. Kept matches from 2000 where both teams had at least 5 earlier games (25,750 matches). Trained on matches before 2023-06-25 (21,886) and tested on the later ones (3,864). Compared always-home, higher-Elo, Logistic Regression and Gradient Boosting.
- **Result:** Logistic Regression reached **60.5% accuracy** and **0.863 log loss** against 47.6% accuracy and 1.051 log loss for always predicting a home win. Its probabilities were well calibrated.

## Results (test set, 3,864 matches)
| Model | Accuracy | Log loss |
|---|---|---|
| Always home win (baseline) | 47.64% | 1.051 |
| Higher Elo wins (with home bonus) | 60.66% | - |
| Logistic Regression | 60.48% | 0.863 |
| Gradient Boosting | 60.48% | 0.866 |

Home-win probability calibration (predicted vs actual): 0.109 vs 0.100, 0.304 vs 0.279, 0.502 vs 0.488, 0.700 vs 0.662, 0.869 vs 0.885.

## Key insights
- The models do **not** beat the simple "higher Elo wins" rule on accuracy (60.5% vs 60.7%). The Elo rating already carries most of the signal, and the models mainly add usable probabilities.
- Draws are almost never predicted (1 of 884 real draws), which is common because a draw is rarely the most likely single outcome.
- Final Elo top 5 from this notebook: Spain 2249, Argentina 2183, England 2160, France 2124, Portugal and Brazil 2064. This is a simple custom Elo, not the official FIFA or Elo ratings.
- Example output: Spain vs Argentina on neutral ground gives home 37.4%, draw 33.1%, away 29.6%.

## Limitations
- Only team strength and form are used, with no squad, injuries or tournament importance.
- Draw prediction is essentially not solved here.

## How to run
1. Open `match_outcome_predictor.ipynb` in Google Colab.
2. Runtime > Run all (data downloads from GitHub automatically).
3. The first data cell should print "real data loaded". Numbers can change slightly if the dataset has new matches since this run.

## Files
- `match_outcome_predictor.ipynb` - executed notebook with outputs
- `requirements.txt`

## Author
Akshat Kesharwani
- Portfolio: https://akshatkesharwani-info.github.io/
- GitHub: https://github.com/akshatkesharwani-info
