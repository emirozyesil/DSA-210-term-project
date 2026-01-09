# DSA210 Term Project  
## Factors Influencing Winning in Professional Basketball (NBA)

---

## 1. Project Proposal & Motivation

Winning an NBA game is the outcome of many interacting in-game factors. While the final score determines the winner, *how* that score is achieved throughout the game is often overlooked. In particular, momentum shifts, shot selection strategies, and physicality (fouls) may play a decisive role in determining game outcomes.

The purpose of this project is to **identify which in-game performance factors are most strongly associated with winning NBA games**, using real historical data. Rather than focusing only on final scores, this project emphasizes *when* and *how* advantages are created during the game.

This project is original in its **focus on third-quarter performance**, **foul imbalance**, and **shot selection patterns**, and in how these factors are jointly analyzed using **data enrichment, hypothesis testing, and machine learning**.

---

## 2. Research Questions & Hypotheses

The analysis is structured around three main research questions.  
Each question is associated with a clear null hypothesis (H₀) and alternative hypothesis (H₁), expressed verbally.

---

### RQ1 — Third Quarter Performance

**Research Question:**  
Do teams that perform better in the third quarter have a higher probability of winning?

- **H₀ (Null Hypothesis):**  
  There is no meaningful difference in third-quarter point differential between winning and losing teams.

- **H₁ (Alternative Hypothesis):**  
  Winning and losing teams differ in their third-quarter point differential.

---

### RQ2 — Fouls and Winning

**Research Question:**  
Does committing more or fewer fouls influence a team’s likelihood of winning?

- **H₀ (Null Hypothesis):**  
  Winning and losing teams commit, on average, the same number of fouls.

- **H₁ (Alternative Hypothesis):**  
  Winning and losing teams commit a different number of fouls on average.

---

### RQ3 — Shot Selection (Three-Point Attempt Ratio)

**Research Question:**  
Does a team’s preference for three-point shots relative to two-point shots affect winning probability?

- **H₀ (Null Hypothesis):**  
  Winning and losing teams have similar three-point attempt ratios.

- **H₁ (Alternative Hypothesis):**  
  The three-point attempt ratio differs between winning and losing teams.

---

## 3. Data Sources

This project uses **two publicly available Kaggle datasets**, selected to enable both game-level and team-level analysis.

---

### Dataset 1 — NBA Match Results (1949–2024)

- **Author:** joybiswas389  
- **Link:** https://www.kaggle.com/datasets/joybiswas389/nba-matches-results-1949-2024  

**Description:**  
Provides match-level information including final scores, quarter-by-quarter scoring, and game outcomes.

**Key variables used:**
- Team names  
- Final scores  
- Quarter scores (Q1–Q4)  
- Game outcomes  

**Role in project:**  
Used to compute:
- Win indicator  
- Final score margin  
- Third-quarter point differential  
- Close-game indicator  

---

### Dataset 2 — Historical NBA Data and Player Box Scores

- **Author:** eoinamoore  
- **Link:** https://www.kaggle.com/datasets/eoinamoore/historical-nba-data-and-player-box-scores  

**Description:**  
Contains player-level box score data for NBA games.

**Key variables used:**
- Field goal attempts (FGA)  
- Three-point attempts (3PA)  
- Personal fouls (PF)  

**Role in project:**  
Player-level statistics are aggregated to the team-game level to construct:
- Total team fouls  
- Total three-point attempts  
- Two-point attempts  
- Shot selection ratios  

---

## 4. Data Cleaning & Preprocessing

Before analysis, several preprocessing steps were applied:

- Converted game timestamps to proper datetime format  
- Standardized team name strings (uppercase, trimmed whitespace)  
- Verified data consistency using:
  - `df.info()`  
  - `df.isna().sum()`  
- Ensured compatibility for dataset merging and self-joins  

These steps ensured data reliability and prevented key mismatches during enrichment.

---

## 5. Data Enrichment (Feature Engineering)

Because the raw datasets do not directly contain all variables needed for analysis, several **custom features** were engineered.

---

### Match-Level Engineered Features

- **final_margin:**  
  Difference between team and opponent final scores  

- **win:**  
  Binary outcome (1 = win, 0 = loss)  

- **Q3_diff:**  
  Third-quarter point differential (team − opponent)  

- **close_game:**  
  Indicator for games decided by 5 points or fewer  

---

### Team-Level Engineered Features

- **team_total_fouls:**  
  Sum of player fouls per team per game  

- **team_total_3PA:**  
  Total three-point attempts  

- **team_total_2PA:**  
  Computed as `FGA − 3PA`  

- **threePA_ratio:**  
  Proportion of three-point attempts among all shot attempts  

- **Foul_diff:**  
  Difference between team fouls and opponent fouls  

These features transform raw statistics into analytically meaningful indicators of strategy, discipline, and momentum.

---

## 6. Exploratory Data Analysis (EDA)

EDA was used to explore distributions, relationships, and potential predictive signals:

- Team-level win rate visualization  
- Boxplots comparing winners vs losers for:
  - Q3_diff  
  - Foul_diff  
  - threePA_ratio  
- Distribution analysis for close games  
- Summary statistics and correlation inspection  

EDA guided the choice of hypothesis tests and informed feature selection for modeling.

---

## 7. Hypothesis Testing

To formally evaluate the research questions, statistical hypothesis tests were conducted.

**Methods used:**
- Two-sample t-tests for mean comparison  
- Normality and variance checks  
- Mann–Whitney U tests where parametric assumptions were violated  

**Interpretation:**
- P-values were compared against α = 0.05  
- Results were interpreted in the context of basketball dynamics rather than purely statistical significance  

This step connects exploratory insights with formal statistical evidence.

---

## 8. Machine Learning: Win Prediction

To complement statistical testing, a supervised learning approach was applied.

### Objective
Predict game outcome (`win`) using engineered in-game features.

### Features Used
- Q3_diff  
- Foul_diff  
- threePA_ratio  
- home  
- close_game  

### Modeling Approach
- Train-test split (80% / 20%), stratified by outcome  
- Logistic Regression with StandardScaler pipeline  
- Evaluation metrics:
  - Accuracy  
  - Confusion matrix  
  - Classification report  

### Interpretability
- Logistic regression coefficients were extracted and visualized  
- Feature importance analysis revealed:
  - **Third-quarter point differential** as the strongest positive predictor of winning  

---

## 9. Project Structure & Reproducibility

Notebooks are organized sequentially and can be run end-to-end:

1. `01_data_cleaning_enrichment.ipynb`  
2. `02_exploratory_data_analysis.ipynb`  
3. `03_hypothesis_testing.ipynb`  
4. `04_machine_learning_models.ipynb`  

Processed datasets are saved to ensure reproducibility and clarity.

---

## 10. Conclusion

This project demonstrates that **when advantages are created during the game matters as much as how large they are**. Third-quarter dominance, disciplined play, and strategic shot selection all show meaningful relationships with winning outcomes.

By combining data enrichment, exploratory analysis, hypothesis testing, and machine learning, the project provides both **statistical evidence** and **predictive insight** into the dynamics of professional basketball games.
