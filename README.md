# DSA210 Term Project  
## Factors Influencing Winning in Professional Basketball

---

## 1. Project Overview

This project investigates **which in-game factors most strongly influence the likelihood of winning NBA basketball games**. Using real match data and player box scores, the goal is to determine whether specific statistics—such as third-quarter performance, total fouls committed, and shot selection patterns—have a significant and measurable impact on game outcomes.

To achieve this, game-level information from NBA match results is combined with player-level box score data. These datasets are cleaned, merged, and enriched to create a unified analytical table suitable for statistical analysis and hypothesis testing.

---

## 2. Research Questions & Hypotheses

Below are the key questions this project aims to answer. Each includes a clear null hypothesis (H₀) and an alternative hypothesis (H₁), expressed verbally (no symbolic formulas).

### **RQ1 — Third Quarter Performance**
**Question:**  
Do winning teams generally perform better in the third quarter compared to losing teams?

- **H₀ (Null):**  
  There is no meaningful difference in third-quarter point differential between winning and losing teams.

- **H₁ (Alternative):**  
  Third-quarter point differential differs between winning and losing teams.

---

### **RQ2 — Fouls and Winning**
**Question:**  
Do teams that commit more or fewer fouls tend to win more often?

- **H₀ (Null):**  
  Winning and losing teams commit, on average, the same number of fouls.

- **H₁ (Alternative):**  
  Winning and losing teams commit a different number of fouls on average.

---

### **RQ3 — Shot Selection (3PA Ratio)**
**Question:**  
Does attempting more three-point shots relative to two-point shots influence a team’s chances of winning?

- **H₀ (Null):**  
  Winning and losing teams have similar three-point attempt ratios.

- **H₁ (Alternative):**  
  The three-point attempt ratio differs between winning and losing teams.

---

## 3. Data Sources

Two public Kaggle datasets are used to build the enriched game-level dataset.

---

### **Dataset 1 — NBA Match Results (1949–2024)**  
**Author:** joybiswas389  
**Link:** https://www.kaggle.com/datasets/joybiswas389/nba-matches-results-1949-2024  

**Purpose:**  
Provides match-level information including team names, final scores, quarter-by-quarter scoring, and game outcomes.

**Key variables used:**
- Team names  
- Final scores  
- Quarter scores (Q1–Q4)  
- Game outcome  
- Match metadata  

**Contribution to project:**  
Allows computation of variables such as:
- third-quarter point differential  
- final score margin  
- win indicator  
- close-game flag  

---

### **Dataset 2 — Historical NBA Data and Player Box Scores**  
**Author:** eoinamoore  
**Link:** https://www.kaggle.com/datasets/eoinamoore/historical-nba-data-and-player-box-scores  

**Purpose:**  
Provides player-level box scores that can be aggregated into team-level statistics for each game.

**Key variables used:**
- Field goal attempts (FGA)  
- Three-point attempts (3PA)  
- Personal fouls (PF)  
- Points and other box score metrics  

**Contribution to project:**  
By aggregating player statistics on a per-team, per-game basis, the following enriched variables can be constructed:
- team total fouls  
- team total 3PA and 2PA  
- team-level 3PA ratio  
- foul differential between teams  
- team shooting profile metrics  

---

## 4. Data Enrichment

Because the datasets are public, custom enrichment is essential.  
The project constructs additional features not directly provided by the raw datasets.

### **Match-level engineered features (from Dataset 1):**
- **final_margin:** difference between team and opponent final scores  
- **win:** binary indicator of victory  
- **Q3_diff:** third-quarter point differential  
- **close_game:** whether the final margin is within 5 points  

### **Team-game-level engineered features (aggregated from Dataset 2):**
- **team_total_fouls:** sum of player fouls for each team in a game  
- **team_total_3PA:** total three-point attempts  
- **team_total_2PA:** computed as FGA minus 3PA  
- **3PA_ratio:** proportion of 3-point attempts relative to all field goal attempts  
- **Foul_diff:** difference in fouls between the two teams in a game  

These enriched features form the basis of the statistical comparisons and hypothesis tests.

---

## 5. Exploratory Data Analysis (EDA)

To understand the behavior of the enriched variables, the project includes:

- Summary statistics for major variables (Q3_diff, fouls, 3PA ratio, final margin)  
- Histograms and distributions  
- Boxplots comparing winners and losers  
- Correlation matrix and heatmap  
- Scatterplots showing relationships between key variables and scoring margins  

EDA helps reveal early patterns and guides the choice of statistical methods.

---

## 6. Hypothesis Testing

For each research question, statistical tests are applied to assess whether differences between winning and losing teams are statistically meaningful.  

Tests include:
- Two-sample t-tests  
- Normality and variance checks  
- Non-parametric alternatives where needed (e.g., Mann–Whitney U test)

These analyses evaluate whether third-quarter performance, total fouls, and shot selection are significantly associated with winning outcomes.

---

