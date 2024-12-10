# League of Legends Predictive Analysis

[![logo](https://brand.riotgames.com/static/a91000434ed683358004b85c95d43ce0/8a20a/lol-logo.png)]
---
## Introduction

[League of Legends](https://en.wikipedia.org/wiki/League_of_Legends) is one of the most popular video games in the world, boasting a massive player base and a thriving, lucrative esports scene. Despite its popularity, the game is notorious for being difficult to master, largely due to the critical importance of the early game. Often regarded as the make-or-break phase where victories are decided, this stage is central to many strategies and discussions. This analysis seeks to uncover whether the early game’s importance is a myth perpetuated by the community or a genuine predictor of match outcomes

**This report** aims to cut through anecdotal claims and rigorously examine whether strong early-game performance genuinely correlates with eventual victory. Is the emphasis on first objectives, early gold leads, and timely experience advantages truly justified? Or are these narratives more myth than math? By analyzing professional match data, we seek to clarify the extent to which early dominance predicts a team’s success.

**Dataset Source:** Our analysis draws from a dataset provided by [Oracle’s Elixir](https://oracleselixir.com/tools/downloads), encompassing approximately 10,000 professional-level esports matches from top-tier leagues such as the LCS, LEC, LCK, and LPL.  

**Central Question:** Do early-game objectives—like securing the first dragon or herald—and establishing resource leads in factors like gold and experience reliably translate into a higher likelihood of winning the match?

**Why It Matters:** Understanding the importance of the early game goes beyond theorycrafting. It informs coaching decisions, enhances commentators’ insights, guides viewers in predicting outcomes during live matches, and even helps regular players refine their strategies.

---

### Dataset Overview

To provide a clearer picture, here is an overview of our cleaned data and the key columns we’ll be examining and using for prediction.

| side   |   total_counters |   avg_pick_win_pct | firstblood   | firstdragon   | firstherald   | firstbaron   | firsttower   | firstmidtower   | firsttothreetowers   |   goldat15 |   xpat15 |   csat15 |   golddiffat15 |   xpdiffat15 |   csdiffat15 |   killsat15 |   assistsat15 |   deathsat15 |   Win |
|:-------|-----------------:|-------------------:|:-------------|:--------------|:--------------|:-------------|:-------------|:----------------|:---------------------|-----------:|---------:|---------:|---------------:|-------------:|-------------:|------------:|--------------:|-------------:|------:|
| Blue   |                1 |           0.486409 | False        | False         | True          | True         | True         | True            | True                 |      22384 |    29220 |      498 |           -530 |        -1671 |          -37 |           0 |             0 |            1 |     1 |
| Red    |                0 |           0.474672 | True         | True          | False         | False        | False        | False           | False                |      22914 |    30891 |      535 |            530 |         1671 |           37 |           1 |             1 |            0 |     0 |
| Blue   |                2 |           0.466322 | False        | False         | True          | True         | False        | True            | True                 |      24771 |    30084 |      498 |            673 |          530 |          -34 |           4 |             6 |            3 |     0 |
| Red    |                1 |           0.514853 | True         | True          | False         | False        | True         | False           | False                |      24098 |    29554 |      532 |           -673 |         -530 |           34 |           3 |             4 |            4 |     1 |
| Blue   |                0 |           0.480499 | False        | False         | False         | False        | False        | True            | False                |      22945 |    27423 |      510 |          -1901 |         -763 |           58 |           2 |             1 |            4 |     1 |

- **Number of Rows:** 21,946 (each match contributes two rows—one for each team)
- **Key Columns:**  
  - **side:** Red or Blue, indicating the team’s starting side.  
  - **total_counters:** The number of counter-picks the opposing team fields, where a counter-pick is a champion selection that outperforms one chosen by the first team. 
  - **avg_pick_win_pct:** The average of all the win percentages of every champion on the selected team
  - **firstblood:** Binary indicator of whether the team secured the first kill of the match.  
  - **firstdragon:** Binary indicator of securing the first dragon.  
  - **firstherald:** Binary indicator of securing the first herald.  
  - **firstbaron:** Binary indicator of securing the first baron.  
  - **firsttower:** Binary indicator of taking down the first tower.  
  - **firsttothreetowers:** Binary indicator of being the first to destroy three towers.  
  - **goldat15:** Numerical value representing the team’s total gold at 15 minutes.  
  - **xpat15:** Numerical value representing the team’s total experience at 15 minutes.  
  - **csat15:** Numerical value representing the team’s total creep score at 15 minutes.  
  - **killsat15:** Numerical value representing the team’s total kills at 15 minutes.  
  - **assistsat15:** Numerical value representing the team’s total assists at 15 minutes.  
  - **deathsat15:** Numerical value representing the team’s total deaths at 15 minutes.
  - **golddiffat15:** Numerical value indicating the gold lead or deficit compared to the opponent at 15 minutes.  
  - **xpdiffat15:** Numerical value indicating the experience lead or deficit at 15 minutes.  
  - **csdiffat15:** Numerical value indicating the creep score lead or deficit at 15 minutes.  
  - **Win:** Binary indicator of whether the team won or lost.  


However, the data was not always this clean. Lets take a look at the data cleaning process.
---

## Data Cleaning and Exploratory Data Analysis

### Cleaning Steps

1. **Missing Value Handling:** Missing values in columns `[X, Y]` were filled using [method, e.g., mean, median, interpolation].
2. **Outlier Removal:** Outliers in `[Column]` were removed using [method, e.g., IQR filtering].
3. **Standardization:** Quantitative variables were standardized to ensure compatibility across scales.
4. **Encoding:** Nominal data in `[Column]` was encoded using one-hot encoding.

### Impact on Analysis

These steps ensured a robust foundation for analysis by minimizing bias and enhancing interpretability.

### Head of Cleaned DataFrame

```plaintext
[Table displaying the cleaned data (5 rows)]
```

---

## Exploratory Visualizations

### Univariate Analysis

<iframe
  src="assets/univariate-plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

**Interpretation:** The distribution of `[Column]` reveals [trend, e.g., normal distribution, skewness], suggesting [key insight].

---

## Bivariate Analysis

<iframe
  src="assets/bivariate-plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

**Interpretation:** The relationship between `[Column X]` and `[Column Y]` shows a [trend, e.g., positive correlation, no clear relationship]. This indicates [relevant insight].

---

## Assessment of Missingness

**NMAR Analysis:** The column `[Column]` is potentially NMAR because [explanation]. Additional data on [specific features] could clarify the missingness mechanism.

### Missingness Permutation Test

<iframe
  src="assets/missingness-plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

**Null Hypothesis:** [State null hypothesis]  
**Alternative Hypothesis:** [State alternative hypothesis]  
**p-value:** [Result]  
**Conclusion:** [Interpret results in the context of your question]

---

## Hypothesis Testing

### Test Results

- **Null Hypothesis:** [State null hypothesis]  
- **Alternative Hypothesis:** [State alternative hypothesis]  
- **Significance Level:** 0.05  
- **Test Statistic:** [Chosen statistic]  
- **p-value:** [Result]  

**Conclusion:** Based on the p-value, we [fail to reject/reject] the null hypothesis, suggesting [conclusion].

---

## Framing a Prediction Problem

**Prediction Type:** [Classification/Regression]  
**Response Variable:** [Variable name]  
**Evaluation Metric:** [Metric and justification]  

**Why This is Important:** This prediction task is crucial for [impact, e.g., operational efficiency, decision-making].

---

## Baseline Model

**Model Description:** [Baseline model and its characteristics]  
**Performance:** [Baseline performance metrics]  

---

## Final Model

**Model Description:** [Final model type and features used]  
**Performance Improvement:** The final model improved upon the baseline by [comparison metrics].  
**Key Features Added:** [Discuss added features and their relevance to the data generating process]

<iframe
  src="assets/model-performance.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

---

## Fairness Analysis

**Groups Analyzed:** [Group X vs. Group Y]  
**Evaluation Metric:** [Metric]  
**Null Hypothesis:** [State null hypothesis]  
**Alternative Hypothesis:** [State alternative hypothesis]  
**Significance Level:** 0.05  
**p-value:** [Result]  

**Conclusion:** [Interpret fairness results]

---

## Conclusion

Thank you for exploring this data analysis project. If you have questions or feedback, feel free to [contact me](mailto:your-email@example.com).
```
