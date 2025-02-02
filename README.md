# Predicting NBA Salaries Using Linear Regression

**STA302H1: Methods of Data Analysis I**
**Final Project**  

**Team Members:**  
- Christoffer Tan
- Janis Joplin 
- Razan Ahsan Rifandi

---

## Overview

This repository contains the code, data, and documentation for our analysis of NBA player salaries. Our study investigates the following research question:

> **To what extent can NBA player performance metrics and achievements predict their salaries using linear regression?**

Using an in-depth multiple linear regression approach (with Box-Cox transformations and automated model selection), we explore how factors such as points, assists, efficiency, positional roles, and All-Star participation contribute to salary determination.

---

## Methodology

1. **Data Exploration and Preparation**
   - Removed 66 observations with missing values.
   - Split the dataset into equal training and test sets (50/50 split).
   - Performed EDA with histograms, boxplots, and barplots to visualize distributions and identify outliers.

2. **Preliminary Modeling**
   - Fitted simple linear regression (SLR) models for each predictor to assess individual relationships with salary.
   - Built a multiple linear regression (MLR) model including all predictors; evaluated significance via t-tests and ANOVA, and checked for multicollinearity using VIF.

3. **Model Refinement**
   - Verified MLR assumptions (linearity, uncorrelated errors, constant variance, and normality).
   - Applied Box-Cox transformations to several variables to correct assumption violations.
   - Reassessed the model assumptions post-transformation.

4. **Model Selection**
   - Employed automated variable selection methods (forward, backward, and stepwise selection using R’s `stepAIC` function) to arrive at the final model.
   - Compared models using adjusted R-squared, AIC, BIC, and AICc.
   - Addressed multicollinearity and removed non-significant predictors based on partial F-tests.

5. **Final Model and Validation**
   - Constructed the final predictive model on transformed training data, then validated it on the test set.
   - Verified consistency of coefficient estimates and ensured that all MLR assumptions were met.
   - Final model predictors include points (PTS), assists (AST), effective field goal percentage (eFG%), positional roles (dummy variables), and All-Star participation.

---

## Key Results

- **Final Model Equation (Transformed):**

  $\sqrt[4]{\text{Salary}} = \beta_0 + \beta_1 \log(\text{PTS}+1) + \beta_2 \left(\frac{1}{\sqrt{\text{AST}+1}}\right) + \beta_3 ((\text{eFG.}+1)^4) + \beta_4 I[\text{Pos1}=PF] + \beta_5 I[\text{Pos1}=PG] + \beta_6 I[\text{Pos1}=SF] + \beta_7 I[\text{Pos1}=SG] + \beta_8 I[\text{Play}=Yes]$

- **Coefficient Summary:**

  | Predictor           | Estimate  | Std. Error | T-value | P-value  |
  |---------------------|-----------|------------|---------|----------|
  | Intercept           | 46.7853   | 5.8911     | 7.942   | < 0.001  |
  | log(PTS + 1)        | 9.8242    | 1.2061     | 8.146   | < 0.001  |
  | 1/√(AST + 1)        | -19.4321  | 5.3472     | -3.634  | < 0.001  |
  | (eFG. + 1)^4        | -0.9147   | 0.428      | -2.137  | 0.033    |
  | Pos1PF              | -5.3281   | 1.282      | 8.146   | < 0.01   |
  | Pos1PG              | -8.918    | 1.627      | -5.481  | < 0.001  |
  | Pos1SF              | -3.9817   | 1.3801     | -2.885  | 0.004    |
  | Pos1SG              | -8.0479   | 1.2697     | -6.339  | < 0.001  |
  | PlayYes             | 6.2993    | 1.94       | 3.247   | 0.0012   |

- **Statistical Insights:**
  - **Scoring Ability (PTS)** emerged as the most significant positive predictor.
  - **Assists (AST)** demonstrated an inverse relationship with salary.
  - **Effective Field Goal Percentage (eFG%)** had a smaller negative effect.
  - **Positional roles** and **All-Star participation** were key salary determinants, with centers generally earning more.

- **Model Performance:**
  - Adjusted R-squared of approximately 0.45 (training) and 0.48 (test), indicating a robust model fit.
  - Diagnostic tests confirmed that linear regression assumptions were largely satisfied after transformation.

---

## Ethical Considerations

The project emphasizes the ethical use of statistical methods, particularly in:
- **Automated Variable Selection:** Utilizing forward, backward, and stepwise selection to reduce human bias.
- **Transparency and Reproducibility:** Documenting the full analysis process and using well-established R libraries.
- **Addressing Statistical Pitfalls:** Preventing harmful practices such as p-hacking and ensuring an objective model-building process.

---

## Limitations and Future Work

- **Data Limitations:** Potential issues with rookie salary caps and variability in player performance.
- **Model Limitations:** The need for data transformations (e.g., Box-Cox) and addressing possible systemic biases.
- **Future Research:** Could explore nonlinear models and incorporate additional contextual factors (e.g., team dynamics, market effects).

---

## Bibliography

- Lyons Jr., R., Jackson Jr., E. N., & Livingston, A. (2015). *Determinants of NBA player salaries*. The Sport Journal.
- Sigler, K. J., & Sackley, W. H. (2000). *NBA players: Are they paid for performance?* Managerial Finance.
- Bodvarsson, O. B., & Brawstow, R. T. (1998). *Do employers pay for consistent performance? Evidence from the NBA*. Economic Inquiry.
- Ratto, Davide. (2019). *NBA Players 2016-2019*. [Data set]. Kaggle.
