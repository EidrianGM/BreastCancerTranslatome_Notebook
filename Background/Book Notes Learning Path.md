- Chemical Manufacturing Process example dataset is very similar to my own data type
### Common Workflow
#### 1. Data Pre-processing
* Addition or deletion of data points
	* Removal of outliers samples and skewed variables
	* Skewness assesment
		* An un-skewed distribution is one that is roughly symmetric. This means that the probability of falling on either side of the distribution’s mean is roughly equal. 
* Data transformations and combinations | Feature engineering
	* Data encoding -> different ways to express a data, i.e. date formats
	* Relationship between predictor and response
		* If outcome depends on season or month, day in 365 format or month is better that month day format.
	* Centering by subtracting the average predictor value   from all its values to obtain a zero mean
	* Scaling the data each value of the predictor variable is divided by its standard deviation coercing the data to have a common standard deviation of one.
* Variables/Predictors selection (adding or removing)
	* Features extraction
		* empirical technique for creating surrogate variables that are combinations of multiple predictors
	* Removal of low informative variables
	* Tree-based models are notably insensitive to the characteristics of the predictor data
	* Linear regressions are very sensitive to predictor data
	* Removing predictors without considering how those variables might be related to the outcome
* Binning continuous variables
* Types of pre-processing:
	* Unsupervised:
		* the outcome variable is not considered by the pre-processing techniques
	* Supervised:
		* the outcome is utilized by the pre-processing
#### 2. Resampling
* Data spending
	* Tune a model
	* Assess its performance
#### 3. Model selection
#### 3.1. Classification of Predictive Models
* Regression -> Predicting continuous variables by
	* Linear combination of predictors
		* Linear regression
		* Partial least squares (PLS)
			* are essentially supervised versions of principal component analysis (PCA)
			* Benefited by centered and scaled data
		* L1 regularization
	* Not based on linear combinations of predictors
		* Neural networks
		* Multivariate adaptive regression splines (MARS)
			* Limitation: 
				* Define the tuning parameter for the equation that determine the number of  different linear models or segments 
		* Support vector machines (SVMs)
		* KNNs
		* Tree-based (ensembl methods)
			* Regression trees
			* Bagged trees
			* Random forests
			* Boosting
			* Cubist
* Classification -> Predicting categorical variables
	* Linear combination of predictors
		* Linear
		* Quadratic (curves in y~x)
		* Regularized
		* Partial least squares discriminant analysis
		* Penalized methods
	* Not based on linear combinations of predictors (highly)
		* Neural networks
		* SVMs
		* KNNs
		* Naı̈ve Bayes
		* Nearest shrunken centroids
		* Tree-based
#### 4. Feature selection methods

#### 5. Model Evaluation
* Resampling (or cross-validation)
	* Different subversions of the training data set are used to fit and evaluate the model
*  Regression
	* Root mean squared error (RMSE)
		* interpreted as how far, on average, the residuals are from zero
* Classification

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
* Splitting into train and test
	* Extrapolating
		* Using different populations or cohorts 
	* Interpolating
		* We pick random subsets:
			* A small test would have limited utility as a judge of performance. In this case, a sole reliance on resampling techniques (i.e.,no test set) might be more effective. 

### Model Selection
* Partial Least Squares
	* Naturally manages correlated predictors but is numerically more stable if the predictors are on similar scales/magnitudes (due to SVD calculations, for example, a predictor with values in the thousands might overshadow another predictor in the range of 0 to 1)
	* Also good if the number of predictors exceeds the number of observations.
* Recursive partitioning
	* Is unaffected by predictors of different scales but has a less stable partitioning structure when predictors are correlated.
	* Can be used when predictors contain moderate amounts of missing information.
* Multiple linear regression 
	* Cannot handle missing predictor information.