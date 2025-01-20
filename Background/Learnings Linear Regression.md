In addition to ordinary linear regression, these types of models include partial least squares (PLS) and penalized models such as ridge regression, the lasso, and the elastic net. Each of these models seeks to find estimates of the parameters so that the sum of the squared errors (SSE) or a function of the sum of the squared errors is minimized. A distinct advantage of these models is that they are highly interpretable.  Furthermore, relationships among predictors can be further interpreted through the estimated coefficients. Also their mathematical nature enables us to compute standard errors of the coefficients, provided that we make certain assumptions about the distributions of the model residuals. These standard errors can then be used to assess the statistical significance of
each predictor in the model. 

#### Linear regression
* At one extreme, finds parameter estimates that have minimum bias
* **Making some minimal assumptions** about the distribution of the residuals, it is straightforward to show that the parameter estimates that minimize SSE are the ones that have the least bias of all possible parameter estimates . **Hence, these estimates minimize the bias component of the bias-variance trade-off.**
* The sum-of-squared errors (SSE):
	* SSE = SUM(yi − ŷ i)² 
* Beta values are proportional to the covariance matrix of the predictors.
* Careful:
	* **A unique inverse of this matrix exists when**  (LM basic assumptions)
		* (1) no predictor can be determined from a combination of one or more of the other predictors. However, a unique set of predicted values can still be obtained for data that fall under this condition (1) by either replacing B coefficients with a conditional inverse or by removing predictors that are collinear. 
		* (2) the number of samples is greater than the number of predictors. If the data fall under either of these conditions, then a unique set of regression coefficients does not exist. 
			* Use pre-processing techniques to filter samples or predictors
	* The upshot of these facts is that linear regression can still be used for prediction when collinearity exists within the data. But since the regression coefficients to determine these predictions are not unique, we lose our ability to meaningfully interpret the coefficients.
* By default, when fitting a linear model with R and collinearity exists among predictors, “. . .R fits the largest identifiable model by removing variables in the reverse order of appearance in the model formula”
* **The variance inflation factor**
	* To diagnose multicollinearity in the context of linear regression
* Another drawback of multiple linear regression is that its solution is linear in the parameters. This means that the solution we obtain is a flat hyperplane.
* One visual clue to understand if the relationship between predictors and the response is not linear is to examine the basic diagnostic plots:
	* Predicted values VS Observed
	* Predicted values VS Residuals
		* Curvature in the predicted-versus-residual plot is a primary indicator that the underlying relationship is not linear.


#### Partial least squares (PLS)

#### Penalized models

##### Ridge Regression
* find estimates that have lower variance
##### Lasso
* find estimates that have lower variance
##### Elastic Net
* find estimates that have lower variance