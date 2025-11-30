# Factors Influencing Winning in Professional Basketball  
### DSA210 – Fall 2025 Term Project

---

## 1. Introduction & Motivation

Basketball fans and analysts often talk about “momentum shifts”, “smart fouling”, and “modern 3-point heavy offenses”, but these are usually based on intuition rather than systematic evidence.  

This project aims to **quantitatively analyze which game statistics are most strongly associated with winning** in professional basketball, using data from the **NBA** and **EuroLeague**.  

I will focus on three specific factors:

1. **Third quarter scoring performance**  
2. **Number of fouls committed**  
3. **Shot selection strategy (2-point vs 3-point attempts)**  

The goal is to move from anecdotal beliefs to **data-driven insights** about how teams actually play when they win.

---

## 2. Problem Definition

The central question of this project is:

> **Which aspects of in-game performance are most strongly associated with winning in professional basketball games?**

To make this question concrete and measurable, I focus on:

- Whether **3rd quarter point differential** is higher for winning teams  
- Whether **foul counts** differ between winning and losing teams  
- Whether **3-point attempt ratio** differs between winning and losing teams  

These questions will be answered using **exploratory data analysis (EDA)** and **statistical hypothesis testing** on game-level data.

---

## 3. Research Questions & Hypotheses

Below are the research questions and their formal hypotheses, written in statistical form with \(H_0\) and \(H_1\).

Let:

- \( Q3\_diff \) = team’s points in Q3 − opponent’s points in Q3  
- \( \text{Fouls} \) = total team fouls in the game  
- \( 3PA \) = three-point field goal attempts  
- \( 2PA \) = two-point field goal attempts  
- \( \text{3PA Ratio} = \dfrac{3PA}{2PA + 3PA} \)  
- Subscripts **win** and **lose** refer to the group of games where the team won or lost.

---

### RQ1 — 3rd Quarter Performance

**Research Question 1:**  
> Do winning teams have a different average 3rd quarter point differential compared to losing teams?

**Hypotheses:**

- **H0 (Q3):**  
  The mean 3rd quarter point differential is the same for winning and losing teams.  
  \[
  \mu_{\text{win}}^{Q3\_diff} = \mu_{\text{lose}}^{Q3\_diff}
  \]

- **H1 (Q3):**  
  The mean 3rd quarter point differential is different for winning and losing teams.  
  \[
  \mu_{\text{win}}^{Q3\_diff} \neq \mu_{\text{lose}}^{Q3\_diff}
  \]

---

### RQ2 — Fouls and Game Outcome

**Research Question 2:**  
> Do teams that commit more fouls tend to win or lose, or is there no meaningful difference?

I will study both **total fouls** and **foul differential** (home vs away).

#### 2.1 Total Fouls (Team Level)

- **H0 (Fouls-Total):**  
  The mean total number of fouls is the same for winning and losing teams.  
  \[
  \mu_{\text{win}}^{Fouls} = \mu_{\text{lose}}^{Fouls}
  \]

- **H1 (Fouls-Total):**  
  The mean total number of fouls is different for winning and losing teams.  
  \[
  \mu_{\text{win}}^{Fouls} \neq \mu_{\text{lose}}^{Fouls}
  \]

#### 2.2 Foul Differential (Optional, Home vs Away)

Let \( Foul\_diff = Fouls_{home} - Fouls_{away} \).

- **H0 (Fouls-Diff):**  
  The distribution of foul differential does not differ between games won and lost by the home team.  
  \[
  \mu_{\text{home\_win}}^{Foul\_diff} = \mu_{\text{home\_lose}}^{Foul\_diff}
  \]

- **H1 (Fouls-Diff):**  
  The foul differential is different between games won and lost by the home team.  
  \[
  \mu_{\text{home\_win}}^{Foul\_diff} \neq \mu_{\text{home\_lose}}^{Foul\_diff}
  \]

---

### RQ3 — Shot Selection: 2-Point vs 3-Point Attempts

**Research Question 3:**  
> Do winning teams have a different shot selection profile, specifically in terms of 3-point attempt ratio, compared to losing teams?

I will use the **3-point attempt ratio** as a measure of shot selection:

\[
\text{3PA Ratio} = \frac{3PA}{2PA + 3PA}
\]

**Hypotheses:**

- **H0 (3PA Ratio):**  
  The mean 3-point attempt ratio is the same for winning and losing teams.  
  \[
  \mu_{\text{win}}^{3PA\ Ratio} = \mu_{\text{lose}}^{3PA\ Ratio}
  \]

- **H1 (3PA Ratio):**  
  The mean 3-point attempt ratio is different for winning and losing teams.  
  \[
  \mu_{\text{win}}^{3PA\ Ratio} \neq \mu_{\text{lose}}^{3PA\ Ratio}
  \]

These hypotheses will be tested separately for NBA and EuroLeague if the datasets allow.

---

## 4. Data Source

I will use **publicly available Kaggle datasets** that contain NBA and EuroLeague game statistics. Examples include (exact links will be added later):

- NBA regular season and/or playoff box score datasets  
- EuroLeague game-level statistics datasets  

Typical variables available in these datasets:

- Game metadata: season, date, game ID, home/away teams  
- Final scores and winner/loser  
- Points scored per quarter (Q1, Q2, Q3, Q4)  
- Fouls committed, free throws  
- Field goal attempts and makes (2PA, 3PA, FGA, FG%)  

### Data Enrichment (Required for Public Data)

Because the data is public, I will **enrich it with additional features**, such as:

- Third quarter point differential: `Q3_diff`  
- Final score differential: `final_margin`  
- Total fouls for each team and foul differential: `Fouls_home`, `Fouls_away`, `Foul_diff`  
- 3PA ratio for each team: `3PA_ratio = 3PA / (2PA + 3PA)`  
- Binary indicators: `win`, `home_win`, `close_game` (e.g., |final_margin| ≤ 5)  

Raw data will be stored in:

```text
data/raw/
