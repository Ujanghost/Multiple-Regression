# Multiple Regression Analysis Report

## 1. Introduction

This report presents a multiple regression analysis performed on a dataset related to soccer player statistics. Multiple regression is a statistical technique that explores the relationship between a dependent variable and two or more independent variables. By analyzing the relationships between these variables, we can gain insights into the factors that influence the dependent variable and make predictions based on the independent variables.

## 2. Dataset Description and Source

The dataset used for this analysis is called "CompleteDataset.csv". It contains information about soccer players, including their personal details, performance metrics, club information, and various attributes related to their skills and abilities. The dataset is sourced from [kaggle](https://www.kaggle.com/datasets/thec03u5/fifa-18-demo-player-dataset).

## 3. AIM/Objective

The primary objective of this analysis is to build a multiple regression model that can effectively predict a player's "Overall" rating based on several predictor variables, such as age, potential, value, and wage. By examining the relationships between these variables and the overall rating, we aim to gain insights into the factors that contribute to a player's overall performance. Additionally, we will assess the adequacy of the model by checking for multicollinearity and heteroscedasticity, two common issues that can affect the reliability of regression models.

## 4. Analysis

The analysis is performed using Python programming language and several libraries, including pandas, statsmodels, matplotlib, and seaborn.

### 4.1. Data Preprocessing

Before fitting the multiple regression model, the data is preprocessed to handle any non-numeric values or missing data. The "Value" and "Wage" columns are converted to numeric format by performing the following steps:

1. Remove the '€' currency symbol using `str.replace('€', '')`.
2. Remove the 'M' (million) and 'K' (thousand) suffixes using `str.replace('M', '')` and `str.replace('K', '')`.
3. Convert the remaining string values to float using `astype(float)`.
4. For the 'Value' column, if a value contains 'K', it is divided by 1000 to convert it to millions, assuming 'K' stands for thousands.

Any missing values in the predictor variables are filled with 0 using the `fillna(0)` method.

### 4.2. Model Fitting

The multiple regression model is fitted using the `statsmodels` library. The target variable is "Overall", and the predictor variables are "Age", "Potential", "Value", and "Wage". A constant term is added to the predictors using `sm.add_constant()` to include the intercept in the model.

The `sm.OLS()` function from the `statsmodels.api` module is used to specify the ordinary least squares (OLS) regression model. The `fit()` method is then called on the resulting OLS model object to fit the model to the data and obtain the parameter estimates.

### 4.3. Model Summary and Diagnostics

The summary of the fitted model is printed using `model.summary()`, displaying the following information:

- Coefficients: The estimated coefficients for each predictor variable.
- Standard Errors: The standard errors of the coefficient estimates.
- t-statistics: The t-statistics for each coefficient, used to assess the statistical significance of the predictors.
- p-values: The p-values corresponding to the t-statistics, indicating the level of significance of each predictor.

This information helps assess the significance of each predictor in explaining the variation in the target variable.

To check for multicollinearity, the Variance Inflation Factors (VIF) are calculated using the formula `1 / (1 - model.rsquared)`. VIF values greater than 5 or 10 may indicate the presence of multicollinearity, which can lead to unstable coefficient estimates and inflated standard errors.

Heteroscedasticity, which refers to non-constant variance of residuals, is checked using the Breusch-Pagan test and White's test from the `statsmodels.stats.diagnostic` module. The `het_breuschpagan` and `het_white` functions are used to perform these tests, respectively. Small p-values (typically less than 0.05) from these tests indicate evidence of heteroscedasticity, which violates one of the assumptions of multiple regression.

### 4.4. Visualizations

Several visualizations are created to explore the data and relationships between variables:

1. **Boxplot**: A boxplot is generated for the target variable ("Overall") to visualize its distribution using `sns.boxplot()` from the seaborn library.
2. **Correlation Heatmap**: A heatmap is created to display the correlation between the numeric variables in the dataset using `sns.heatmap()` and the `corr()` method from pandas.
3. **Group Plot**: A scatter plot is generated, showing the relationship between "Overall" and "Age", with points colored based on the "Potential" rating using `sns.scatterplot()` with the `hue` parameter.
4. **Parallel Plot**: A parallel plot is created to visualize the selected features ("Overall", "Age", "Potential", "Value", "Wage") simultaneously using `pd.plotting.parallel_coordinates()` from the pandas library.

These visualizations provide valuable insights into the data and aid in understanding the relationships between variables, as well as identifying potential outliers or patterns.
## 5. Conclusion

The multiple regression analysis provides insights into the relationships between various player attributes and their overall performance rating. By assessing the model's adequacy through multicollinearity and heteroscedasticity checks, we can ensure the reliability of the results and identify potential issues that may require further investigation or alternative modeling techniques.

The visualizations generated in this analysis offer valuable visual representations of the data, allowing for better understanding of variable distributions, correlations, and relationships between different features.

### 6.References 

[1]seaborn, “seaborn: statistical data visualization — seaborn 0.9.0 documentation,” Pydata.org, 2012. https://seaborn.pydata.org/
[2]Wikipedia Contributors, “Regression analysis,” Wikipedia, Mar. 22, 2019. https://en.wikipedia.org/wiki/Regression_analysis
‌[3]“Working with missing data — pandas 1.5.1 documentation,” pandas.pydata.org. https://pandas.pydata.org/docs/user_guide/missing_data.html
