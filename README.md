# Statistical Modelling of U.S. Medical Insurance Costs

Statistical modelling project in **R** focused on explaining variation in annual medical insurance costs using demographic and health-related characteristics.

The project develops and refines a multiple regression model, evaluates nonlinear and interaction effects, performs regression diagnostics, and compares the final specification with a **Gamma Generalized Linear Model (GLM)** designed for positive and heteroscedastic cost data.

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

The baseline model provides a reference specification from which transformations, interactions, and nonlinear effects can be evaluated.

### 2. Log Transformation of Medical Costs

The distribution of `charges` is strongly right-skewed.

A logarithmic transformation improves the shape of the response distribution and the overall regression fit. The analysis therefore adopts:

```text
log(charges)
```

as the dependent variable for the main linear model.

This also allows many coefficients to be interpreted approximately in percentage terms.

### 3. Interaction Effects

Two interaction terms are introduced:

- `smoker × bmi`
- `smoker × age`

Both interactions are statistically significant.

This allows the relationship between smoking and insurance costs to vary with the individual's age and BMI rather than assuming a constant additive smoking effect.

Including these interactions also improves the model-selection criteria relative to the simpler specification.

### 4. Nonlinear Effects

The relationships between medical cost and both `age` and `bmi` were examined for nonlinear behavior.

Quadratic effects were evaluated for both predictors. Subsequent model comparison showed that an alternative transformation provided a better specification for age, while a quadratic term for BMI was retained.

### 5. Predictor Transformations

A logarithmic transformation of age was compared with the quadratic-age specification.

The model using `log(age)` achieved similar explanatory power while improving AIC and BIC.

The final specification therefore uses:

- `log(age)`
- `bmi`
- `bmi²`
- smoking interactions
- demographic controls

## Final Linear Model

The final specification can be summarized as:

```text
log(charges) ~
    children
  + smoker
  + log(age)
  + bmi
  + sex
  + region
  + bmi²
  + smoker:bmi
  + smoker:log(age)
```

The final model achieves:

- **R² = 0.8286**
- **Adjusted R² = 0.8272**
- **Global F-statistic = 582.8**
- **p-value < 2.2 × 10⁻¹⁶**

Approximately **83% of the observed variation in log medical costs** is explained by the variables included in the model.

Among the specifications evaluated, the final model also achieves the best overall balance between fit and complexity according to **AIC and BIC**.

## Regression Diagnostics

Model quality was evaluated beyond goodness-of-fit metrics.

### Residual Structure

Residual-vs-fitted plots suggest that the mean relationship is reasonably well captured, although larger residual dispersion appears for some lower fitted values.

### Residual Normality

The Q-Q plot and Shapiro-Wilk test indicate departures from normality, particularly in the upper tail.

Several observations exhibit medical costs substantially higher than predicted by the linear model.

### Heteroscedasticity

The Breusch-Pagan test rejects the null hypothesis of constant variance:

```text
p-value ≈ 1.8 × 10⁻¹¹
```

This provides strong evidence of heteroscedasticity in the final log-linear model.

### Multicollinearity

Adjusted GVIF values remain low across predictors.

The largest values are approximately:

- `log(age)` ≈ 1.72
- `bmi` ≈ 1.77

These values are well below conventional thresholds associated with problematic multicollinearity.

### Residual Dependence

A Durbin-Watson test was used to evaluate residual dependence.

The resulting:

```text
p-value = 0.3851
```

provides no evidence of residual autocorrelation.

## Gamma GLM Benchmark

Because medical insurance costs are:

- strictly positive
- right-skewed
- heteroscedastic

a **Gamma Generalized Linear Model with log link** was also fitted.

The model assumes:

```text
charges ~ Gamma

log(E[charges | X]) = Xβ
```

Unlike classical linear regression, the Gamma specification allows the conditional variance to change with the conditional mean.

This makes it a natural alternative for modelling positive and skewed cost data.

## OLS vs Gamma GLM

The two approaches highlight an important modelling trade-off.

| Model | Reported Adjusted R² | Breusch-Pagan p-value | Main Advantage |
|---|---:|---:|---|
| Log-linear OLS | **0.8272** | ~1.8 × 10⁻¹¹ | Stronger explanatory fit |
| Gamma GLM | **0.7215** | **0.44** | Better variance specification |

Under the diagnostic used, the Gamma GLM no longer shows evidence of the heteroscedasticity observed in the log-linear model.

However, the log-linear OLS specification achieves substantially stronger explanatory fit in this analysis.

The OLS model is therefore retained as the primary specification, while the Gamma GLM serves as an alternative distributional framework and robustness benchmark.

## Key Findings

- Log-transforming medical costs substantially improves the linear-model specification.
- Smoking status is strongly associated with insurance costs, with its effect interacting with age and BMI.
- The relationship between BMI and medical cost is nonlinear.
- A log transformation of age improves the final specification relative to the alternatives evaluated.
- The final OLS model explains approximately **83% of the observed variation in log medical costs**.
- The model shows no problematic multicollinearity or residual autocorrelation.
- Heteroscedasticity and non-normal upper-tail residuals remain important limitations of the linear specification.
- A Gamma GLM better accommodates the variance structure observed in the data, although with lower reported explanatory fit in this analysis.

## Statistical Methods

- Multiple Linear Regression
- Log-Linear Models
- Interaction Effects
- Polynomial Terms
- Variable Transformations
- Generalized Linear Models
- Gamma Regression
- Log Link Functions
- AIC / BIC Model Selection
- Residual Diagnostics
- Breusch-Pagan Test
- Durbin-Watson Test
- Variance Inflation Factors / GVIF
- Shapiro-Wilk Test

## Technologies

- **R**
- Statistical modelling
- Regression analysis
- Generalized Linear Models
- Model diagnostics
- Data visualization

## Project Context

Academic statistical modelling project developed as part of the **Telecommunications Engineering & Business Analytics** program at ICAI – Universidad Pontificia Comillas.
