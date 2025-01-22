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
	* Alternatively, using PCA for pre-processing guarantees that the resulting predictors, or combinations thereof, will be uncorrelated. BUT IN THIS CASES USE PLS
* Another drawback of multiple linear regression is that its solution is linear in the parameters. This means that the solution we obtain is a flat hyperplane.
* One visual clue to understand if the relationship between predictors and the response is not linear is to examine the basic diagnostic plots:
	* Predicted values VS Observed
	* Predicted values VS Residuals
		* Curvature in the predicted-versus-residual plot is a primary indicator that the underlying relationship is not linear.
		* Study the introduction of predictors transformed to quadratic or cubic.  But the larger the number of original predictors, the less practical including some or all of these terms becomes.
		* If easily identifiable nonlinear relationships exist between the predictors and the response, then those additional predictors can be added to the descriptor matrix. 
* Multiple linear regression is prone to chase observations that are away from the overall trend of the majority of the data.
	* **Recall that linear regression seeks to find the parameter estimates that minimize SSE; hence, observations that are far from the trend of the majority of the data will have exponentially large residuals.** 
	* In order to minimize SSE, linear regression will adjust the parameter estimates (BETA / SLOPES) to better accommodate these unusual observations.
		* Observations that cause significant changes in the parameter estimates are called influential, and the field of robust regression has been developed to address these kinds of problems.
	* If this happens often in the data:
		* Use an alternative metric to SSE that is less sensitive to large outliers.
			* Finding parameter estimates that minimize the sum of the absolute errors is more resistant to outliers
			* the Huber function uses the squared residuals when they are “small” and the simple different between the observed and predicted values when the residuals are above a threshold. 
	* If different individual predictors reach the same coefficient/slope with a similar standard error but then when used together for the modelling each individual slope is very different from their individual fit and the standard error increases, the predictors can show colinearity and instability of the model
#### Partial least squares (PLS)
Used if the correlation among predictors is high, then the ordinary least squares solution for multiple linear regression will have high variability and will become unstable.
 * Pre-processing predictors via PCA prior to performing regression is known as principal component regression (PCR) - OBSOLETE TOWARDS PLS
	 * applied in 
		 * the context of problems with inherently highly correlated predictors 
		 * or problems with more predictors than observations
 
* PLS
	* **PLS finds components that maximally summarize the variation of the predictors while simultaneously requiring these components to have maximum correlation with the response.**
	* Require the predictors to be centered and scaled
	* Even with the constraint of correlation with the response, it will be more naturally drawn towards predictors with large variation.
	* algorithm iteratively seeks to find underlying, or latent, relationships among the predictors which are highly correlated with the response.
	* For a univariate response, each iteration of the algorithm assesses the relationship between the predictors (X) and response (y) and numerically summarizes this relationship with a vector of weights (w) also known as a direction;
	* The predictor data are then orthogonally projected onto the direction to generate scores (t). 
	* The scores are then used to generate loadings (p)  which measure the correlation of the score vector to the original predictors.
	* At the end of each iteration, the predictors and the response are “deflated” by subtracting the current estimate of the predictor and response structure, respectively. The new deflated predictor and response information are then used to generate the next set of weights, scores, and loadings. These quantities are sequentially stored in matrices W, T, and P, respectively, and are used for predicting new samples and computing predictor importance. 
	* PLS therefore strikes a compromise between the objectives of predictor space dimension reduction and a predictive relationship with the response. In other words, PLS can be viewed as a supervised dimension reduction procedure; PCR is an unsupervised procedure.
	* Because the latent variables from PLS are constructed using linear combinations of the original predictors, it is more difficult to quantify the relative contribution of each predictor to the model.
		* **variable importance in the projection
			* The predictors and the response can be adequately summarized by a one-component PLS model
			* The importance of predictor is then proportional to the value of the normalized weight vector, w, corresponding to the jth predictor.
			*  When more predictors are involved the numerator of the importance of the jth predictor is a weighted sum of the normalized weights corresponding to the jth predictor.  The jth normalized weight of the kth component, wkj , is scaled by the amount of variation in the response explained by the kth component.
			* Therefore, the larger the normalized weight and amount of response variation explained by the component, the more important predictor is in the PLS model.
			* The larger the VIP value, the more important the predictor is in relating the latent predictor structure to the response. By its construction, the squared VIP values sum to the total number of predictors. As a rule-of-thumb, VIP values exceeding 1 are considered to contain predictive information for the response.
			* 
* Variations
	* NIPALS
		* for data sets of small-to-moderate size (e.g., < 2,500 samples and < 30 predictors). Higher samples or predictors it becomes inefficient.
	* SIMPLS
		* SIMPLS latent variables are identical to those from NIPALS when there is only one response.
	* when n >> P
		* second kernel algorithm of Dayal and MacGregor was more computationally efficient than all other approaches and provided superior performance when n > 2, 500 and P > 30
	* GIFI approach
		* splits each predictor into two or more bins for those predictors that are thought to have a nonlinear relationship with the response.
### Penalized models
Under standard assumptions, the coefficients produced by ordinary least squares regression are unbiased and, of all unbiased linear techniques, this model also has the lowest variance. Given that MSE is combination of variance and bias, it is very possible to produce models with smaller MSEs by allowing the parameter estimates to be biased. 
* A small increase in bias can produce a substantial drop in the variance and thus a smaller MSE than ordinary least squares regression coefficients. 
* One consequence of large correlations between the predictor variances is that the variance can become very large. Combatting collinearity by using biased models may result in regression models where the overall MSE is competitive.
* The penalties require tuning to achieve optimal performance.
##### Types
* **Ridge Regression**
	* Requires the predictors centered and scaled prior to this analysis so that their units are the same. 
	* adds a penalty on the sum of the squared regression parameters
	* In effect, this method shrinks the estimates towards 0 as the λ penalty becomes large but it is never 0
	* Even though some parameter estimates become negligibly small, this model does not conduct feature selection
* **Lasso (least absolute shrinkage and selection operator)**
	* the regression coefficients are still shrunk towards 0 but
	* a consequence of penalizing the absolute values is that some parameters are actually set to 0 for some value of λ
	* models that simultaneously use regularization to improve the model and to conduct feature selection
	* Variants with
		* Linear discriminant analysis
		* PLS
		* PCA
		* LARS (least angle regression)
			*  used to fit lasso models more efficiently, especially in high-dimensional problems
* **Elastic Net** (generalised variant of LASSO)
	* combines the two types of penalties towards 0 and to 0
	* enables effective regularization via the ridge-type penalty with the feature selection quality of the lasso penalty
	* effectively deal with groups of high correlated predictors.
