- Chemical Manufacturing Process example dataset is very similar to my own data type
### Common Workflow
#### 1. Data Pre-processing
* Addition or deletion of data points
	* Removal of outliers samples and skewed variables
* Data transformations and combinations | Feature engineering
	* Data encoding -> different ways to express a data, i.e. date formats
		* Relationship between predictor and response
			* If outcome depends on season or month, day in 365 format or month is better that month day format.
	* Centering by subtracting the average predictor value   from all its values to obtain a zero mean
	* Scaling the data each value of the predictor variable is divided by its standard deviation coercing the data to have a common standard deviation of one.
	*  Skewness assessment
		* An un-skewed distribution is one that is roughly symmetric. This means that the probability of falling on either side of the distribution’s mean is roughly equal. 
		* A general rule of thumb to consider is that skewed data whose ratio of the highest value to the lowest value is greater than 20 have significant skewness. 
		* The skewness statistic can be used as a diagnostic. If the predictor distribution is roughly symmetric, the skewness values will be close to zero.
		* Replacing the data with the log, square root, or inverse may help to remove the skew. Box and Cox family of transformations indexed by a parameter, denoted as λ estimated using maximum likelihood. This procedure would be applied independently to each predictor data that contain values greater than zero.
	* Data Transformations for Multiple Predictors
		* Resolve outliers
			* Samples that are exceptionally far from the mainstream of the data
				* If a model is sensitive to outliers, one data transformation, after centering and scaling, predictor data that can minimize the problem is the spatial sign. Removing predictor variables after applying the spatial sign transformation may be problematic.
			* Predictive models that are resistant to outliers:
				* Tree-based classification
				* SVM
				* 
		* Dimension reduction (signal extraction or feature extraction)
			* PCA (unsupervised)
				* Seek linear combination of predictors that maximize variability
				* With the great advantage that creates components uncorrelated
				* Drawn to summarize predictors that have more variation to lower variation. 
				* Thus different scales and units, will cause variables of high magnitudes be summarized in initial PCs.
					* It means that PCA will be focusing its efforts on identifying the data structure based on measurement scales rather than based on the important relationships within the data for the current problem.
					* to help PCA avoid summarizing distributional differences and predictor scale information, it is best to first transform skewed predictors and center and scale the predictors
				* Scree plot to decide the number of PC to retain based on the number prior to the tapering off of variation.  In an automated process, the optimal number can be determined by cross-validation
				* Recommendation to plot PCAs with the same scale.
				* Loadings, the linear model coefficients, close to zero indicate that the predictor variable did not contribute much to that component. 
			* PLS (supervised)
				* Derive components while simultaneously considering the corresponding response.
* Variables/Predictors selection (adding or removing)
	* Features extraction
		* empirical technique for creating surrogate variables that are combinations of multiple predictors
	* Removal of low informative variables
	* Tree-based models are notably insensitive to the characteristics of the predictor data
	* Linear regressions are very sensitive to predictor data
	* Removing predictors is normally advantageous
		* Careful removing without considering how those variables might be related to the outcome
		* If two are highly correlated remove one because they can be measuring the same underlying information leading to a more parsimonious and interpretable model. 
		* 0 variance predictors
			* Degenerate distributions variables (a random variable has a fixed value with probability 1, and the probability of all other values is 0)
			* Some models, NOT TREEs, can be crippled by these, e.g. linear regression
		* “near-zero variance predictors”
			* have only a handful of unique values that occur with very low frequencies or may have a single value for the vast majority of the samples
			* Careful with this in resampling given that samples with very unique values in the variable might be introduced
			* A small percentage of unique values is, in itself, not a cause for concern as many “dummy variables” generated from categorical predictors would fit this description.
			* The problem occurs when the frequency of these unique values is severely disproportionate. The ratio of the most common frequency to the second most common reflects the imbalance in the frequencies.
				* Remove as variable if
					* The fraction of unique values over the sample size is low (say 10 %).
					* The ratio of the frequency of the most prevalent value to the frequency of the second most prevalent value is large (say around 20).
the second most prevalent value is large (say around 20).
* Binning continuous variables
* Types of pre-processing:
	* Unsupervised:
		* the outcome variable is not considered by the pre-processing techniques
	* Supervised:
		* the outcome is utilized by the pre-processing
* Missing values
	* Nature:
		* Structurally missing (impossible things)
		* Missed Not At Random
		* Missed At Random
	* Informative missingness
		* The pattern of missing data is related to the outcome response variable?
		* A bias source
	* Not the same as censored data (not the exact value but similar, i.e. a time measurement not final, or detection limits)
		* statistical models focused on interpretation or inference, take the censoring into account in a formal manner by making assumptions about the censoring mechanism
		* predictive models treat these data as simple missing data or use the censored value as the observed value
	* Are more often related to predictor variables than the sample thus may be concentrated in a subset of predictors rather than occurring randomly
	* Handling NAs
		* Tree-based models can handle them
		* Imputation methods
			* should be incorporated within the resampling if used
			* If a variable with missing values is highly correlated with another predictor that has few missing values, a focused model can often be effective for imputation e.g. KNN
* Correlation between predictors - Collinearity and multicollinearity.
	* 
	* 
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