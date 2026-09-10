# Statistical Modelling of U.S. Medical Insurance Costs

Statistical modelling project in **R** focused on explaining variation in annual medical insurance costs using demographic and health-related characteristics.

The project develops and refines a multiple regression model, evaluates nonlinear and interaction effects, performs extensive regression diagnostics, and compares the final specification with a **Gamma Generalized Linear Model (GLM)** designed for positive and heteroscedastic cost data.

## Project Overview

The objective is to study the determinants of annual medical insurance charges in the United States.

The dataset contains **1,338 observations**, with insurance cost (`charges`) as the response variable and several demographic and health-related predictors.

The analysis follows an iterative model-development process:

1. Explore and preprocess the dataset
2. Fit an initial multiple linear regression
3. Transform the response variable
4. Introduce interaction and nonlinear effects
5. Compare alternative specifications using information criteria
6. Perform regression diagnostics
7. Compare the final OLS specification with a Gamma GLM

## Dataset

The main variables include:

- `charges` — annual medical insurance cost
- `age` — age of the insured individual
- `bmi` — body mass index
- `children` — number of dependent children
- `smoker` — smoking status
- `sex` — sex of the insured individual
- `region` — U.S. region of residence

Exploratory analysis identified substantial right-skewness in `charges`, motivating further investigation of transformations and alternative distributional assumptions.

## Model Development

### 1. Baseline Multiple Regression

The analysis begins with a multiple linear regression using the available explanatory variables.

The baseline model provides a reference specification from which transformations, interactions and nonlinear effects can be evaluated.

### 2. Log Transformation of Medical Costs

The distribution of `charges` is strongly right-skewed.

A logarithmic transformation substantially improves the shape of the response distribution and the overall regression fit.

The analysis therefore adopts:

```text
log(charges)
