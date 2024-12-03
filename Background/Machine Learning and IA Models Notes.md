## Linear Regressions
- Statistical model that analyzes the relationship between a response variable (often called y) and one or more variables and their interactions (often called x or explanatory variables)
- When a regression takes into account two or more predictors to create the linear regression, it’s called multiple linear regression.
- Basic formula:
	- Result | Expected | Target = Intercept + (Variable|Predictor) * Slope
		- Intercept = base line measurement
		- Variable | Predictor =  (~clinical, ~technical, ~cell populations, ...)
		- Slope = measures the change of results according to variable
- Assumption:
### Assumptions:
In order to interpret the results of the regression analysis meaningfully, certain conditions must be met.
- **Linearity:** There must be a linear relationship between the dependent and independent variables.
- **Homoscedasticity:** The residuals must have a constant variance.
- **Normality:** Normally distributed error
- **No multicollinearity:** No high correlation between the independent variables
- **No auto-correlation:** The error component should have no auto correlation
	- In our context, figure out which variables explain the amount of mRNA being translated (~clinical, ~technical, ~cell populations, ...)
#### Results indexes / coefficients:
- Intercept 
- The base line for our target prediction
- Variable (the slope)
		- In our case if the variable slope is positive or negative, indicates positive or negative correlation or regulation
- Residuals
		- Show the differences between the real values and the predicted values. The idea here is that the sum of the residuals is approximately zero or as low as possible. In real life, most cases will not follow a perfectly straight line, so residuals are expected.
- Model Fit Testing
	- R² (coefficient of determination)
		- Proportion of the total variability explained by the regression model.
		- Models that fit the data well, R² is near 1.
		- Remember: 
			- A high R² is not necessarily good every single time 
			- A low R² is not necessarily always bad. 
			- In some fields, an R² of 0.5 is considered good and 0.7 very good.
			- One problem is that it cannot decrease as you add more independent variables to your model, it will continue increasing as you make the model more complex, even if these variables don’t add anything to your predictions. 
	- R² Adjusted - for multiple variable models 
		- It only increases if the model reduces the overall error of the predictions.
### R::lm()
- Plot the Residuals
```r
	lmTemp = lm(Pressure~Temperature, data = pressure) 
	plot(pressure, pch = 16, col = "blue") #Plot the results
	abline(lmTemp) #Add a regression line
```
* Ideally, when you plot the residuals, they should look random. Otherwise means that maybe there is a hidden pattern that the linear model is not considering. To plot the residuals, use the command `plot(lmTemp$residuals)`
		* This can be a problem. If you have more data, your simple linear model will not be able to generalize well. In the previous picture, notice that there is a pattern (like a curve on the residuals). This is not random at all. 
			* What you can do is a transformation of the variable. Many possible transformations can be performed on your data, such as adding a quadratic term (x²), a cubic (x³), or even more complex such as ln(X), ln(X+1), sqrt(X), 1/x, Exp(X). The choice of the correct transformation will come with some knowledge of algebraic functions, practice, trial, and error. You can apply this directly to the model calculation. Create a linear regression with a quadratic coefficient:
				`lmTemp2 = lm(Pressure~Temperature + I(Temperature^2), data = pressure)`
* Detect influential points or outliers (in our case samples)
	* Technical errors and biasses. Data points where the observed response does not appear to follow the pattern established by the rest of the data.
	* Looking at the object containing the linear model, using the function `cooks.distance()` and then plot these distances. 
		```r
		lmHeight3 = lm(height~age, data = ageandheight)
		summary(lmHeight3) #Review the results
		plot(cooks.distance(lmHeight3), pch = 16, col = "blue") 
		```
		* If a point does not follow the pattern and affects the model:
			1. It is a measurement error or batch effect
				-> Remove the outlier ??
			1. The data point is perfectly valid, in which case the model cannot account for the behavior 
				-> Linear models might not be the correct model ??
#### Step wise regression
**Stepwise regression** is a method of selecting predictors in a linear regression model by adding or removing variables iteratively, based on specific statistical criteria. The primary goal is to identify a subset of explanatory variables that provides the best fit for the data without overfitting or including unnecessary predictors.

Stepwise regression can be used in both **forward** and **backward** directions or as a combination of both, and it is commonly applied when dealing with datasets that contain many potential predictors.
### **Types of Stepwise Regression**

1. **Forward Selection**: -> Is this the one used by Inci?
    - Starts with no predictors in the model (just the intercept).
    - Iteratively adds the most statistically significant variable (e.g., with the lowest p-value) at each step.
    - Stops when no remaining variables meet the inclusion criterion (e.g., p-value < 0.05 or another threshold).
2. **Backward Elimination**:
    - Starts with all candidate predictors in the model.
    - Iteratively removes the least significant variable (e.g., with the highest p-value) at each step.
    - Stops when all remaining variables meet the retention criterion.
3. **Stepwise Selection** (Hybrid Approach):
    - Combines forward selection and backward elimination.
    - At each step, a variable can be added (if it improves the model) or removed (if it becomes insignificant when a new variable is added).
    - This balances between adding important predictors and removing redundant ones.
#### **Criteria for Stepwise Regression**

The inclusion or exclusion of predictors is typically based on:

- **P-values**: Statistical significance of the predictors.
- **AIC (Akaike Information Criterion)**: A measure of model quality that balances goodness of fit and model complexity.
- **BIC (Bayesian Information Criterion)**: Similar to AIC but penalizes more for model complexity.
- **R² or Adjusted R²**: Measures of the proportion of variance explained by the model.
### **Advantages**

1. Simplifies model selection, especially in datasets with many variables.
2. Helps to identify key predictors when there’s no prior knowledge of their importance.
3. Can reduce overfitting by removing unnecessary variables.
### **Limitations**

1. **Overfitting Risk**: May select variables that fit the training data well but do not generalize.
2. **Bias in Variable Selection**: Stepwise methods rely heavily on p-values, which can lead to instability.
3. **Collinearity Issues**: Correlated predictors can lead to arbitrary inclusion/exclusion of variables.
4. **Missed Interactions**: Stepwise methods typically consider individual predictors, not their interactions.

```R
# Full model with all predictors 
full_model <- lm(y ~ x1 + x2 + x3 + x4, data = my_data) 
# Stepwise regression (both directions) 
stepwise_model <- step(full_model, direction = "both") 
# Forward selection 
forward_model <- step(lm(y ~ 1, data = my_data), scope = list(lower = ~1, upper = ~x1 + x2 + x3 + x4), direction = "forward") 
# Backward elimination 
backward_model <- step(full_model, direction = "backward")
```