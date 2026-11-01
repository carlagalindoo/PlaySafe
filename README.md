# PlaySafe

PlaySafe is a machine learning project that estimates the **probability that a LaLiga player will have at least one injury in the next season**. It uses data from previous seasons (player characteristics, playing time and injury history).

The project was made by Carla Galindo for the Practice Challenge.

## Why this project?

Injuries affect the performance of a team, the plans of the coach and the finances of a club. A simple warning tool can help the technical staff (sports scientists, physical trainers and medical staff) to adapt the training and the rotation of the players. The probabilities are **estimates, not certainties**, and they should not be used to decide contracts or playing time.

## Project structure

```
PlaySafe/
├── data/
│   ├── raw/               # original dataset (laliga_players.csv)
│   └── processed/         # cleaned data and test set
├── models/                # trained models (log_reg.joblib, random_forest.joblib)
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── EDA.ipynb
│   ├── IterationZero_Model.ipynb
│   ├── FinalIteration_Model.ipynb
│   └── MVP_Demo.ipynb
├── docs/                  # portfolio documents (LO1–LO5)
├── requirements.txt
└── README.md
```

## How to run the project

Run the notebooks **in this order**, because each one uses the files created by the previous one.

1. `01_data_cleaning.ipynb`: cleans the original dataset and saves `laliga_cleaned.csv`.
2. `EDA.ipynb`: explores the cleaned data.
3. `IterationZero_Model.ipynb`: first model (k-NN), used as a starting point.
4. `FinalIteration_Model.ipynb`: builds the final models (Logistic Regression and Random Forest) and saves them in `models/`.
5. `MVP_Demo.ipynb`: prototype that loads the models and predicts the injury risk of a player.

### Installation

```
pip install -r requirements.txt
```

Then open the notebooks with Jupyter:

```
jupyter notebook
```

## Data

The project uses the `laliga_players.csv` dataset from the [football-injury-scraper](https://github.com/) repository on GitHub. It contains information about LaLiga players, their seasons, minutes played and recorded injuries.

The cleaned data has one row per injury, so the final notebook groups it into **one row per player and season**.

## Method

- **Problem type:** supervised binary classification with probability estimation.
- **Target:** `has_injury_next_season` (1 = at least one injury in the following season, 0 = no injury).
- **Features:** height, position, age in the season, minutes played, number of injuries, days out and matches missed.
- **Validation:** time-based split. The models train with the seasons up to 21/22 and are tested with the seasons 22/23 to 24/25, so the future is never used to predict the past.
- **Models:** Logistic Regression and Random Forest, with the default settings (no tuning).
- **Metrics:** accuracy, precision, recall and F1-score. Recall is especially important because the goal is to find as many players at risk as possible.

## Results

Iteration Zero (k-NN): accuracy 0.529, precision 0.609, recall 0.158, F1-score 0.251.

Final iteration: *(add here the table of the final notebook)*

| Model | Accuracy | Precision | Recall | F1-score |
|---|---|---|---|---|
| Logistic Regression | | | | |
| Random Forest | | | | |

## MVP

The notebook `MVP_Demo.ipynb` is a simple prototype. The user gives the data of a player and gets:

- the probability of injury given by each model,
- a risk level based on the Random Forest (below 40% low, 40–60% medium, above 60% high),
- a comparison with what really happened for real players of the test seasons.

## Limitations

- Injuries have many causes and the dataset does not include things such as training load or GPS data.
- About 100 values of `matches_missed` are missing and are counted as 0. A missing injury is assumed to mean "no injury".
- The same players appear in the training and test seasons, so the model may partly recognise players.
- The models are not tuned and have not been tested with real data from a club.

## Ethics

The dataset contains health information about named players. Predictions should only be used as a warning for the technical staff, never to decide contracts or playing time, and the data must be handled following GDPR.

## Author

Carla Galindo
