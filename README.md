# Tennis Match Outcome Classification

An analysis of how serving statistics relate to recorded ATP match outcomes, combining machine learning with a tennis coach's interpretation of individual matches.

**This is retrospective classification.** The models use statistics from completed matches. Their accuracy does not measure the ability to forecast an unplayed match.

[Read the notebook](tennis_project.ipynb)

## Approach

- Combine ATP match records from 2014–2016 and validate both players' statistics.
- Represent each match as two observations, with a shared match identifier.
- Keep both players together in the training/test split and Random Forest cross-validation.
- Compare Logistic Regression, baseline and tuned Random Forests, and Gradient Boosting on the same held-out matches.
- Interpret global feature rankings and exact Logistic Regression contributions for three named match examples.

## Results

The preparation retains **8,107 of 8,785 matches**, producing 16,214 player-match observations and 14 model features. The test set contains **1,622 matches / 3,244 player observations**.

| Model | Test accuracy | Macro F1 |
|---|---:|---:|
| Logistic Regression | 78.95% | 0.789 |
| Random Forest baseline | 78.91% | 0.789 |
| Tuned Random Forest | 78.79% | 0.788 |
| Gradient Boosting | 78.76% | 0.788 |

The full accuracy range corresponds to only six player observations. These results do not establish a meaningful ranking between the models.

Total serve points won rate receives the highest importance in the tree-based models. The match examples illustrate why strong serving can coexist with a loss and why comparing opponents and return performance provides useful context. Model contributions explain calculations, not the causes of a sporting result.

## Files

```text
tennis_project.ipynb
requirements.txt
data/
  atp_matches_2014.csv
  atp_matches_2015.csv
  atp_matches_2016.csv
images/
  tennis_1.jpeg
```

## Run locally

Tested with Python 3.12.5. Start in the project folder so that the notebook can find `data/` and `images/`.

Create an environment and install dependencies. On Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Open the project folder in VS Code with the Python and Jupyter extensions installed. Open `tennis_project.ipynb`, select the `.venv` Python kernel, and run the notebook from top to bottom.

The Random Forest search evaluates 54 configurations over three grouped folds, so this step takes longer than the rest of the notebook. The code uses CPU-based training.

## Scope and limitations

- Match statistics are available after play, not before the match.
- Metrics are per player observation; each match contributes two related rows.
- Players can appear in both training and test data, and evaluation uses one random grouped split rather than a chronological split.
- Correlated counts and derived rates complicate coefficient and importance interpretation.
- Missing/invalid matches are excluded, while match-completion status is not a general exclusion rule.
- Serve placement, speed and spin are not measured. The error rate cannot be attributed to those factors from these data.

The notebook's final section outlines a separate historical matchup explorer and a possible future forecasting study using lagged features and chronological evaluation.

## Data and image credits

The source repository credits **Jeff Sackmann / Tennis Abstract** as the creator of the ATP match dataset.

The CSV files used in this project were downloaded from the [Kadantte/tennis_atp fork](https://github.com/Kadantte/tennis_atp):

- [2014 ATP matches](https://github.com/Kadantte/tennis_atp/blob/master/atp_matches_2014.csv)
- [2015 ATP matches](https://github.com/Kadantte/tennis_atp/blob/master/atp_matches_2015.csv)
- [2016 ATP matches](https://github.com/Kadantte/tennis_atp/blob/master/atp_matches_2016.csv)

The source repository distributes the dataset under the [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International license (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/). Credit the original creator, retain this license notice, use the data for noncommercial purposes, and share adapted data under the same license. See the [source repository's license notice](https://github.com/Kadantte/tennis_atp#license).

This notebook filters incomplete or invalid statistical records, reshapes each retained match into two player observations, and derives serving rates. These transformations are documented in the notebook. The data license continues to apply to the dataset and its adaptations.

The tennis photograph is Alex Balica's own image.

## Author

Alex Balica — Professional Tennis Coach, Boca Bridges Racquet Club.
