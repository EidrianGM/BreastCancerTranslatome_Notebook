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
	* Adding Predictors
		* Decompose general categorical values into more specific if possible
		* When working with dummy variables 0/1 variables grouping samples
			* Models that include an intercept term, such as simple linear regression, would have numerical issues if each dummy variable was included in the model because they all add up to one and this would provide the same information as the intercept. 
				* For insensitive models, no intercept, including all dummy variables is helpful
		* Adding transformed predictors into no linear relations
		* Adding complex combinations of variables
* Binning continuous variables
	* Simplifying the data into categories that are ranges of values
	* Commonly used in classification issues
		* Ability to make seemingly simple statements, either for sake of having a simple decision rule or the belief that there will be a simple interpretation of the model.
		* The modeler does not have to know the exact relationship between the predictors and the outcome.
		* To obtain a higher response rate for survey questions where the choices are binned.
	* There are many issues with the manual binning of continuous data.
		* Loss of performance and precision
		* Produce a high rate of false positives
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
	* If in a PCA a PC has a high percentage of the variance, this can imply that there is at least one group of predictors that represent the same information.
	* Redundant predictors frequently add more complexity to the model than information they provide to the model.
		* Using highly correlated predictors in techniques like linear regression can result in highly unstable models, numerical errors, and degraded predictive performance. To detect it in use:
			* For linear regression a statistic called the variance inflation factor (VIF). However  it does not determine which predictor should be removed to resolve the problem.
			* remove the minimum number of predictors to ensure that all pairwise correlations are below a certain threshold e.g. 0.75 for sensitive models to correlation
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

####  Train and Test and Model Selection
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

### Over-Fitting
* When the model has also learned the characteristics of each sample’s unique noise of the specific training data used.
* Re-predicting the training set is referred to apparent performance of the model (e.g., the apparent error rate).

### Model Tuning

* Modern approaches to model building split the data into multiple training and testing sets, which have been shown to often find more optimal tuning parameters and give a more accurate representation of the model’s predictive performance
* Tuning parameter is  a parameter that has no analytical formula available to calculate its appropriate value, e.g. the K-nearest neighbor
	* Bad choices might lead to poor performance or over-fitting 
	* There are methods based on resampling to obtain the tuning parameters

#### Data Splitting
* The “training” data set is the general term for the samples used to create the model, while the “test” or “validation” data set is used to qualify performance.
* When a large amount of data is at hand, a set of samples can be set aside to evaluate the final model.
* When the number of samples is not large, a strong case can be made that a test set should be avoided because every sample may be needed for model building.
	* Resampling methods, such as cross-validation.
* Nonrandom approaches to splitting the data are sometimes appropriate. For example:
	* If a model used to predict patient outcomes, the model may be created using certain patient sets (e.g., from the same clinical site or disease stage), and then tested on a different sample population to understand how well the model generalizes.
	* In chemical modeling for drug discovery, new “chemical space” is constantly being explored. We are most interested in accurate predictions in the chemical space that is currently being investigated rather than the space that was evaluated years prior. The same could be said for spam filtering; it is more important for the model to catch the new spamming techniques rather than prior spamming schemes.
* However, in most cases, there is the desire to make the training and test sets as homogeneous as possible. 
	* **Simple random sampling methods can be used**
		* When one class has a disproportionately small frequency compared to the others, there is a chance that the distribution of the outcomes may be substantially different between the training and test sets.
	* **Stratified random sampling applies random**
		* Sampling within subgroups. In this way, there is a higher likelihood that the outcome distributions will match. When the outcome is a number, a similar strategy can be used; the numeric values are broken into similar groups (e.g., low, medium, and high) and the randomization is executed within these groups.
	* **Split on the basis of the predictor values**
		* Maximum dissimilarity sampling.  Dissimilarity between two samples can be measured in a number of ways. The simplest method is to use the distance between the predictor values for two samples. If the distance is small, the points are in close proximity. Larger distances between points are indicative of dissimilarity. To use dissimilarity as a tool for data splitting, suppose the test set is initialized with a single sample. The dissimilarity between this initial sample and the unallocated samples can be calculated. The unallocated sample that is most dissimilar would then be added to the test set. To allocate more samples to the test set, a method is needed to determine the dissimilarities between groups of points.
			* One approach is to use the average or minimum of the dissimilarities
* A subset of samples are used to fit a model and the remaining samples are used to estimate the efficacy of the model. This process is repeated multiple times and the results are aggregated and summarized.
* **k-Fold Cross-Validation** (normally 10)
	* The choice of k is usually 5 or 10, but there is no formal rule. 
		* As k gets larger, the difference in size between the training set and the resampling subsets gets smaller. As this difference decreases, the bias of the technique becomes smaller 
			* (i.e., the bias is smaller for k = 10 than k = 5). 
			* In this context, the bias is the difference between the estimated and true values of performance.
	* Uncertainty (i.e., variance or noise)
		* An unbiased method may be estimating the correct value (e.g., the true theoretical performance) but may pay a high price in uncertainty. 
		* This means that repeating the resampling procedure may produce a very different value (but done enough times, it will estimate the true value). k-fold cross-validation generally has high variance compared to other methods and, for this reason, might not be attractive. It should be said that for large training sets, the potential issues with variance and bias become negligible.
	* Types
		* Random
			* samples are randomly partitioned into k sets of roughly equal size
			* A model is fit using the all samples except the first subset (called the first fold)
			* The held-out (first fold) samples are predicted by this model and used to estimate performance measures.
		* Stratified
			* makes the folds balanced with respect to the outcome 
		*  leave-one-out cross-validation
			* Only one sample is held-out at a time, the final performance is calculated from the k individual held-out predictions. 
* **Generalized Cross-Validation - GCV (For linear regression models)**
	* To approximate the leave-one-out error rate
* **Repeated Training/Test Splits**
	* “leave-group-out cross-validation” or “Monte Carlo cross-validation”
	*  splits data into modeling and prediction sets a defined number of repetitions 
	* Resampling bias decreases as the amount of data in the subset approaches the amount in the modeling set. 
	* A good rule of thumb is about 75–80 %. Higher proportions are a good idea if the number of repetitions is large.
	*  Increasing the number of subsets/repetitions has the effect of decreasing the uncertainty of the performance estimates.
	*  However, to get stable estimates of performance, it is suggested to choose a larger number of repetitions (say 50–200). This is also a function of the proportion of samples being randomly allocated to the prediction set; the larger the percentage, the more repetitions are needed to reduce the uncertainty in the performance estimates.
* **The Bootstrap**
	* A bootstrap sample is a random sample of the data taken with replacement 
	* As a result, some samples will be represented multiple times in the bootstrap sample while others will not be selected at all. The samples not selected are usually referred to as the “out-of-bag” samples. For a given iteration of bootstrap resampling, a model is built on the selected samples and is used to predict the out-of-bag samples.
	* Bootstrap error rates tend to have less uncertainty than k-fold cross-validation. 
		* But it has a similar bias to k-fold cross-validation when k ≈ 2.
		* If the training set size is small, this bias may be problematic, but will decrease as the training set sample size becomes larger.
	* The “632 method”
		* creating a performance estimate that is a combination of the simple bootstrap estimate and the estimate from re-predicting the training set
		* The modified bootstrap estimate reduces the bias, but can be unstable with small samples sizes.
		* This estimate can also result in unduly optimistic results when the model severely over-fits the data, since the apparent error rate will be close to zero.
* Recommendations:
	* A unique test set is a single evaluation of the model and has limited ability to characterize the uncertainty in the results.
	* Proportionally large test sets divide the data in a way that increases bias in the performance estimates.
	* With small sample sizes:
		* The model may need every possible data point to adequately determine model values.
		* The uncertainty of the test set can be considerably large to the point where different test sets may produce very different results.
	* Resampling methods can produce reasonable predictions of how well the model will perform on future samples.
	* No resampling method is uniformly better than another;
		* If the samples size is small, we recommend repeated 10-fold cross-validation for several reasons: the bias and variance properties are good and, given the sample size, the computational costs are not large. 
		* If the goal is to choose between models, as opposed to getting the best indicator of performance, a strong case can be made for using one of the bootstrap procedures since these have very low variance.
		* For large sample sizes, the differences between resampling methods become less pronounced, and computational efficiency increases in importance. Here, simple 10-fold cross-validation should provide acceptable variance, low bias, and is relatively quick to compute.

#### Choosing Final Tuning Parameters
* The “one-standard error” method for choosing simpler models finds the numerically optimal value and its corresponding standard error and then seeks the simplest model whose performance is within a single standard error of the numerically best value.
* There is a potential bias that can occur when estimating model performance during parameter tuning (variables selection).
	* Suppose that the final model is chosen to correspond to the tuning parameter value associated with the smallest error rate. This error rate has the potential to be optimistic since it is a random quantity that is chosen from a potentially large set of tuning parameters.
### Choosing Between Models
* Discover the “performance ceiling”
	1. Start with several models that are the least interpretable and most flexible, such as boosted trees or support vector machines. Across many problem domains, these models have a high likelihood of producing the empirically optimum results (i.e., most accurate).
	2. Investigate simpler models that are less opaque (e.g., not complete black boxes), such as multivariate adaptive regression splines (MARS), partial least squares, generalized additive models, or naı̈ve Bayes models.
	3. Consider using the simplest model that reasonably approximates the performance of the more complex methods.

### Interpretation
* When evaluating the accuracy of a model, the baseline accuracy rate to beat would be 70 % 


## Measuring Performance in Regression Models
#### Quantitative Measures of Performance
1. **The root mean squared error (RMSE)**
	* Lower values the better
	* The square root of the mean squared error (MSE) 
		* The MSE is calculated by squaring the residuals and summing them.
	* The value is usually interpreted as either how far (on average) the residuals are from zero or as the average distance between the observed values and the model predictions.
2. **Coefficient of determination (R2)**
	* Interpreted as the proportion of the information in the data that is explained by the model
	* R2 is a measure of correlation, not accuracy
	* R2 is dependent on the variation in the outcome
		* At the same RMSE 
			* R2 is proportional to the variance of the outcome/response variable
				* Bigger variance in the response variable produce bigger R2 and low produces low 
3.  **Rank correlation between the observed and predicted values**
	* When the importance is the ranking position given by the model
	* The rank correlation takes the ranks of the observed outcome values (as opposed to their actual numbers) and evaluates how close these are to ranks of the model predictions. To calculate this value, the ranks of the observed and predicted outcomes are obtained and the correlation coefficient between these ranks is calculated. This metric is commonly known as Spearman’s rank correlation.
#### The Variance-Bias Trade-off
Models commonly have either high bias or high variance. It is generally true that more complex models can have very high variance, which leads to over-fitting. On the other hand, simple models tend not to over-fit, but under-fit if they are not flexible enough to model the true relationship (thus high bias).Also, highly  correlated predictors can lead to collinearity issues and this can greatly increase the model variance.

If we assume that the data points are statistically independent and that the residuals have a theoretical mean of zero and a constant variance of σ2 , then
E[MSE] = σ² + (Model Bias)² + Model Variance.
* E is the expected value
* σ² is usually called “irreducible noise” and cannot be eliminated by modeling.
* The second term is the squared bias of the model. This reflects how close the functional form of the model can get to the true relationship between the predictors and the outcome.
