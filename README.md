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

## 8. Machine Learning Analysis

The purpose of the machine learning stage is not only to predict game outcomes, but also
to **quantify how strongly each in-game factor contributes to winning**.
While hypothesis tests evaluate variables individually, machine learning allows us to
observe their combined effect in a predictive setting.

### Problem Definition
The task is formulated as a **binary classification problem**:
- **Target variable:** `win` (1 = win, 0 = loss)

This setup allows us to examine whether engineered in-game features can jointly explain
and predict game outcomes.

---

### Feature Selection Rationale

The following features were selected based on insights from EDA and hypothesis testing:

- **Q3_diff**  
  Captures third-quarter momentum, which is often considered a turning point in games.
- **Foul_diff**  
  Represents physical discipline and free-throw opportunities.
- **threePA_ratio**  
  Reflects offensive shot selection strategy.
- **home**  
  Accounts for home-court advantage.
- **close_game**  
  Controls for high-variance situations where outcomes may be less predictable.

These features are interpretable, game-related, and directly linked to the research questions.

---

### Train–Test Split

To evaluate generalization performance, the dataset was split into:
- **80% training data**
- **20% test data**

Stratified sampling was used to preserve the win–loss distribution in both subsets.
This prevents biased evaluation caused by class imbalance.

---

### Model Choice: Logistic Regression

Logistic Regression was selected as the baseline model for three main reasons:

1. **Interpretability**  
   The model provides coefficients that directly indicate the direction and magnitude
   of each feature’s effect on winning probability.

2. **Statistical consistency**  
   Logistic Regression aligns well with the hypothesis-testing framework already applied
   earlier in the project.

3. **Simplicity and robustness**  
   It serves as a strong baseline before introducing more complex models.

Feature scaling was applied using a `StandardScaler` within a pipeline to ensure
numerical stability and fair coefficient comparison.

---

### Model Evaluation

The model was evaluated on the held-out test set using:
- Accuracy
- Confusion matrix
- Precision, recall, and F1-score

The Logistic Regression model achieved an accuracy of approximately **68.5%**,
indicating that the selected in-game features contain meaningful predictive information
about game outcomes.

---

### Model Interpretation

To understand *why* the model makes its predictions, logistic regression coefficients
were extracted and analyzed.

Key observations:
- **Q3_diff** has the strongest positive coefficient, confirming that outperforming the
  opponent in the third quarter substantially increases winning probability.
- **Home-court advantage** also contributes positively, consistent with prior basketball
  literature.
- **Foul_diff** shows a negative association, suggesting that committing more fouls than
  the opponent may reduce winning chances.
- **threePA_ratio** exhibits a smaller but noticeable effect, indicating that shot
  selection alone is not sufficient but still relevant.

These findings are consistent with the earlier EDA and hypothesis testing results,
providing cross-validation across analytical methods.

---

### Summary of Machine Learning Insights

The machine learning analysis confirms that:
- Third-quarter performance is the most influential factor in determining NBA game outcomes.
- Winning is best explained by a **combination** of momentum, discipline, and context
  rather than a single statistic.
- Simple, interpretable models can provide strong explanatory power when paired with
  thoughtful feature engineering.

Overall, machine learning complements statistical testing by demonstrating how multiple
in-game factors interact to shape winning probabilities.

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

This study set out to understand **which in-game factors most strongly influence winning in NBA basketball** by combining data enrichment, exploratory analysis, hypothesis testing, and machine learning.

The results consistently point to **third-quarter performance** as the most critical determinant of game outcomes. Both statistical tests and machine learning models show that teams gaining an advantage in the third quarter significantly increase their probability of winning. This highlights the importance of mid-game momentum, adjustments made after halftime, and execution during the early second half.

Foul-related variables provide additional insight. While fouls alone do not determine outcomes, committing more fouls than the opponent is generally associated with lower winning probability. This suggests that discipline and avoiding unnecessary fouls can indirectly impact game results by affecting free-throw opportunities and defensive stability.

Shot selection, measured through the three-point attempt ratio, shows a more nuanced relationship with winning. While higher reliance on three-point shooting is not a guaranteed path to victory, it remains a meaningful contextual factor that interacts with other aspects of team performance rather than acting independently.

From a modeling perspective, the machine learning analysis confirms that **winning is best explained by a combination of factors rather than any single statistic**. Logistic Regression demonstrates that interpretable models, when paired with carefully engineered features, can provide both predictive power and clear insights into game dynamics.

Overall, this project demonstrates that **when advantages are created during a game matters as much as how large those advantages are**. Teams that control the third quarter, maintain discipline, and apply balanced offensive strategies are more likely to secure wins. The integrated analytical approach used in this study provides a structured framework for understanding basketball performance beyond final scores and offers a foundation for future extensions using more advanced models or play-by-play data.



## Use of AI Tools

AI-based tools (including large language models) were used to assist with
some of code structuring, and improving clarity of explanations.


