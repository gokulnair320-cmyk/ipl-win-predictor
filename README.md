#  IPL Live Win Probability Predictor

A machine learning project that predicts the **live win probability** of IPL matches ball by ball, built using the IPL dataset from Kaggle.

---

##  Project Overview

This project predicts the probability of a team winning at any point in an IPL match based on the current match situation. It uses two separate models — one for each innings — since the dynamics of setting a score vs chasing a target are fundamentally different.

---

##  Model Architecture

| Innings | Model | Accuracy |
|---|---|---|
| Innings 1 (Setting) | Random Forest | ~90% |
| Innings 2 (Chasing) | XGBoost | ~99% |

Two models are used intentionally:
- **Innings 1** — No target exists yet, model predicts based on scoring rate and wickets
- **Innings 2** — Target is known, model uses chase dynamics like required run rate, balls remaining etc.

---

##  Dataset

- **Source:** [IPL Dataset - Kaggle](https://www.kaggle.com/datasets/manasgarg/ipl/data)
- **Files used:** `matches.csv`, `deliveries.csv`
- **Preprocessing:** Removed DL affected matches, super overs, and irrelevant columns

---

## ⚙️ Features Used

**Innings 1:**
- Batting team, Bowling team
- Over, Balls bowled
- Cumulative runs, Cumulative wickets
- Current run rate, Extra runs

**Innings 2 (all of above plus):**
- Target, Runs required
- Balls remaining, Required run rate

---

##  How to Use
```python
# Innings 1 example
predict_win_probability(
    innings=1, batting_team='Mumbai Indians', bowling_team='Chennai Super Kings',
    over=18, balls_bowled=108, cumulative_runs=200, cumulative_wickets=0,
    extra_runs=0, current_run_rate=11.1
)

# Innings 2 example
predict_win_probability(
    innings=2, batting_team='Mumbai Indians', bowling_team='Chennai Super Kings',
    over=15, balls_bowled=90, cumulative_runs=120, cumulative_wickets=4,
    extra_runs=3, current_run_rate=8.0, target=165,
    balls_remaining=30, runs_required=46, required_run_rate=9.2
)
```

**Output:**
```
Batting Team (Mumbai Indians) Win Probability: 72.00%
Bowling Team (Chennai Super Kings) Win Probability: 28.00%
```

---

##  Tech Stack

- Python
- Pandas, NumPy
- Scikit-learn
- XGBoost
- Google Colab

---

##  Key Design Decisions

- **No player features** — model focuses on match situation, not individual players, making it truly live and generalizable
- **No venue/toss features** — pre-match context becomes irrelevant once the game is in progress
- **Separate models per innings** — avoids confusing the model with fundamentally different contexts
- **Label Encoding** for team names — cleaner than one-hot encoding for tree-based models

---

##  Future Plans

- [ ] Ball by ball win probability graph
- [ ] Live commentary generator using Claude API
- [ ] Drama score — rates match excitement in real time
- [ ] Web app deployment using Flask/Streamlit
- [ ] "What needs to happen" predictor

---

## 👤 Author

Made with ❤️ and cricket knowledge
