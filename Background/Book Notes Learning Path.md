- Chemical Manufacturing Process example dataset is very similar to my own data type
- 
#### Data splitting Train and Test and Model Selection
* Relationship between the number of samples (n) and number of predictors (P)
	* High n - low P (n > P)
		* handled by all predictive models
	* Low n - high P (n < P)
		* Multiple linear regression or linear discriminant analysis cannot be directly used
		* However recursive partitioning and K-nearest neighbors can be used 
* Response variable:
	* Distribution 
		* Continuous: symmetric or skewed
		* Categorical: balanced or unbalanced
* Predictor variables dependencies:
	* Missing values
	* Correlation among them
	* Their sparseness (a majority of samples contain the same information while only a few contain unique information)
	* Distribution 
		* Continuous: symmetric or skewed
		* Categorical: balanced or unbalanced
	* Underlying relationship with response
		* Yes or No?
### Model Selection
* Partial Least Squares
	* Naturally manages correlated predictors but is numerically more stable if the predictors are on similar scales/magnitudes (due to SVD calculations, for example, a predictor with values in the thousands might overshadow another predictor in the range of 0 to 1)
	* Also good if the number of predictors exceeds the number of observations.
* Recursive partitioning
	* Is unaffected by predictors of different scales but has a less stable partitioning structure when predictors are correlated.
	* Can be used when predictors contain moderate amounts of missing information.
* Multiple linear regression 
	* Cannot handle missing predictor information.