# Hypothesis Testing Case Study

## Overview
This repository contains a hypothesis testing case study performed in Python. The study involves statistical analysis to test assumptions and validate claims using hypothesis testing techniques. The analysis includes data exploration, assumption checks, and statistical tests, ensuring robust conclusions.

## Dataset
The dataset used in this study includes multiple variables related to the hypothesis being tested. The key attributes include:
- **Independent Variables:** [Specify relevant variables]
- **Dependent Variable:** [Specify target variable]
- **Categorical and Continuous Features:** [Mention key features]

## Libraries Used
```python
import pandas as pd
import numpy as np
import scipy.stats as stats
import matplotlib.pyplot as plt
import seaborn as sns
```

## Data Loading and Exploration
We begin by loading the dataset and performing exploratory data analysis (EDA) to understand the data distribution and identify missing values.

```python
data = pd.read_csv('data.csv')
print(data.info())
print(data.describe())
```

## Hypothesis Testing Process
### Step 1: Define Hypotheses
We formulate the null (**H₀**) and alternative (**H₁**) hypotheses based on the problem statement.

Example:
- **H₀:** There is no significant difference between group means.
- **H₁:** There is a significant difference between group means.

### Step 2: Check Assumptions
Before performing hypothesis testing, we check for normality and homogeneity of variance.

#### Normality Test
Using the Shapiro-Wilk test:
```python
stat, p_value = stats.shapiro(data['column_name'])
print(f'Statistic={stat}, p-value={p_value}')
```
- If `p-value > 0.05`, data follows a normal distribution.
- If `p-value <= 0.05`, data does not follow a normal distribution.

#### Homogeneity of Variance Test
Using Levene’s test:
```python
stat, p_value = stats.levene(data['group1'], data['group2'])
print(f'Statistic={stat}, p-value={p_value}')
```
- If `p-value > 0.05`, variances are equal.
- If `p-value <= 0.05`, variances are not equal.

### Step 3: Perform Hypothesis Test
#### T-test (for comparing two means)
```python
t_stat, p_val = stats.ttest_ind(data['group1'], data['group2'], equal_var=True)
print(f'T-statistic={t_stat}, p-value={p_val}')
```
- If `p-value <= 0.05`, reject H₀ (significant difference exists).
- If `p-value > 0.05`, fail to reject H₀ (no significant difference).

#### ANOVA (for comparing more than two groups)
```python
f_stat, p_val = stats.f_oneway(data['group1'], data['group2'], data['group3'])
print(f'F-statistic={f_stat}, p-value={p_val}')
```

#### Chi-Square Test (for categorical data)
```python
contingency_table = pd.crosstab(data['category1'], data['category2'])
chi2_stat, p, dof, expected = stats.chi2_contingency(contingency_table)
print(f'Chi2-stat={chi2_stat}, p-value={p}')
```

### Step 4: Interpret Results
- If the `p-value` is less than 0.05, we reject the null hypothesis, indicating a statistically significant effect.
- Otherwise, we fail to reject the null hypothesis, meaning there is insufficient evidence to support the alternative hypothesis.

## Visualizations
We use visualizations to support our findings.

#### Boxplot to Compare Groups
```python
sns.boxplot(x='category', y='value', data=data)
plt.title('Boxplot of Groups')
plt.show()
```

#### Histogram for Distribution
```python
sns.histplot(data['column_name'], bins=30, kde=True)
plt.title('Data Distribution')
plt.show()
```

## Conclusion
The hypothesis testing case study provided insights into the statistical significance of differences between groups. The results help in making data-driven decisions based on the analyzed patterns. Further analysis can be performed by incorporating additional tests or adjusting sample sizes for robustness.


