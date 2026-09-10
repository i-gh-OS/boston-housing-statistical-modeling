# Statistical Modelling of Boston Housing Prices

Statistical modelling project in **R** focused on explaining variation in Boston housing prices through multiple regression, model specification, nonlinear effects and regression diagnostics.

The project develops an initial multiple linear regression model and progressively refines its specification using transformations, interaction terms, polynomial effects and information criteria.

## Project Overview

The objective is to model the relationship between housing prices and a set of socioeconomic, environmental and urban characteristics.

Rather than fitting a single regression specification, the project follows an iterative statistical modelling process:

1. Build a baseline multiple linear regression model
2. Evaluate model specification
3. Transform variables where appropriate
4. Introduce interaction and nonlinear effects
5. Compare competing specifications
6. Diagnose violations of regression assumptions

The final specification explains approximately **83% of the observed variation in housing prices**.

## Model Development

### 1. Baseline Multiple Regression

The analysis begins with a multiple linear regression containing the available explanatory variables.

The baseline model provides a reference specification from which alternative models can be evaluated.

Variables and specifications are subsequently compared using statistical significance and model-selection criteria.

### 2. Response Transformation

A logarithmic transformation of the dependent variable was evaluated to improve model specification.

Using `log(medv)` instead of housing prices in levels substantially improved model fit:

- Adjusted R² increased from approximately **0.735 to 0.784**
- AIC decreased from **3023.7 to -232.0**
- BIC decreased from **3078.7 to -177.1**

The logarithmic specification was therefore retained for subsequent model development.

### 3. Interaction Effects

Two interaction effects were investigated:

- `rm × lstat`
- `nox × dis`

The `rm × lstat` interaction was highly statistically significant, indicating that the relationship between the number of rooms and housing value depends on the socioeconomic characteristics of the neighborhood.

The interaction model improved adjusted R² to approximately **0.811** and further reduced both AIC and BIC.

### 4. Nonlinear Effects

Exploratory analysis suggested nonlinear relationships between housing prices and several explanatory variables.

Quadratic terms were evaluated for:

- `rm²`
- `lstat²`

The inclusion of `rm²` improved model-selection criteria, while the quadratic `lstat` term did not provide sufficient improvement.

The final specification therefore retained the nonlinear effect in `rm`.

### 5. Predictor Transformations

Logarithmic transformations were evaluated for skewed explanatory variables.

Transforming crime rate did not improve the model and was therefore rejected.

In contrast, replacing `dis` with `log(dis)` improved model performance:

- AIC: **-322.6**
- BIC: **-254.9**
- Adjusted R²: approximately **0.821**

This transformation was retained in the final model.

## Final Model

The final specification combines:

- Multiple linear regression
- Log-transformed response variable
- Log-transformed predictor
- Interaction effects
- A quadratic term
- Model selection using AIC and BIC

The final model achieves approximately:

**R² ≈ 0.83**

meaning that roughly 83% of the observed variation in housing prices is explained by the variables included in the model.

## Interpretation of Selected Effects

### Crime Rate

Higher crime rates are associated with lower housing values, holding the remaining variables constant.

### Distance to Employment Centers

Because distance enters the model logarithmically, its coefficient can be interpreted approximately in elasticity terms.

A 1% increase in distance to employment centers is associated with an approximately **0.41% decrease** in expected housing value, conditional on the remaining variables and interaction effects.

### Number of Rooms

The inclusion of `rm²` indicates that the effect of additional rooms is nonlinear rather than constant across housing sizes.

### Rooms × Socioeconomic Status

The interaction between `rm` and `lstat` shows that the effect of additional rooms varies across neighborhoods.

The positive effect associated with larger homes becomes weaker as `lstat` increases.

## Model Selection

Competing model specifications were evaluated using:

- Adjusted R²
- Akaike Information Criterion (**AIC**)
- Bayesian Information Criterion (**BIC**)
- Log-likelihood

These criteria were used jointly to balance explanatory performance against increasing model complexity.

The final specification achieved the best overall combination of goodness of fit and model parsimony among the alternatives considered.

## Regression Diagnostics

Model assumptions were evaluated rather than treating goodness of fit as sufficient evidence of model quality.

### Residual Analysis

Residual-vs-fitted and Q-Q plots were used to evaluate functional form and the residual distribution.

The residuals were broadly centered around zero but displayed departures from ideal regression assumptions, particularly in the tails.

### Heteroscedasticity

The **Breusch-Pagan test** strongly rejected the null hypothesis of constant residual variance.

The model therefore exhibits heteroscedasticity.

### Multicollinearity

Variance Inflation Factors (**VIF**) were analyzed to assess multicollinearity.

No variables showed severe multicollinearity under the VIF > 10 criterion, although moderate multicollinearity was identified for some predictors.

### Residual Dependence

Residual dependence was also examined.

The diagnostic statistic suggested some positive autocorrelation, indicating that the model may not capture every systematic component of the data.

### Residual Normality

A Shapiro-Wilk test rejected exact normality of the residuals.

However, graphical analysis indicated an approximately symmetric residual distribution, with the main departures occurring in the tails.

## Key Findings

- Model specification substantially improved after transforming the response variable.
- Interaction terms captured relationships that could not be represented by purely additive effects.
- A quadratic room effect provided evidence of nonlinearity.
- `log(dis)` improved the final specification, while transforming crime rate did not.
- The final model explains approximately **83% of housing-price variation**.
- AIC, BIC and log-likelihood favored the final specification over the alternatives considered.
- Diagnostic testing revealed heteroscedasticity, moderate multicollinearity in some predictors and departures from residual normality.

## Methodology

- Multiple Linear Regression
- Interaction Effects
- Polynomial Regression Terms
- Log Transformations
- Model Specification
- AIC / BIC Model Selection
- Log-Likelihood
- Residual Diagnostics
- Breusch-Pagan Test
- Variance Inflation Factors
- Shapiro-Wilk Test

## Technologies

- **R**
- Statistical modelling
- Regression analysis
- Model diagnostics
- Data visualization

## Project Context

Academic statistical modelling project developed as part of the **Telecommunications Engineering & Business Analytics** program at ICAI – Universidad Pontificia Comillas.
