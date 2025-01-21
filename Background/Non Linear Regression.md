# Support Vector Machines (SVMs)

* centering and scaling the predictors prior to building an SVM model. 
* framework of robust regression
	* seek to minimize the effect of outliers on the regression equations
* €-insensitive regression.
	* SVMs for regression use a function similar to the Huber function, with an important difference. Given a threshold set by the user (denoted as €) data points with residuals within the threshold do not contribute to the regression fit while data points with an absolute difference greater than the threshold contribute a linear-scale amount
	* First, since the squared residuals are not used, large outliers have a limited effect on the regression equation. 
	* Second, samples that the model fits well (i.e., the residuals are small) have no effect on the regression equation. 
	* In fact, if the threshold is set to a relatively large value, then the outliers are the only points that define the regression line! This is somewhat counterintuitive: the poorly predicted points define the line. However, this approach has been shown to be very effective in defining the model.
* Tuning
	* The cost parameter is the main tool for adjusting the complexity of the model. When the cost is large, the model becomes very flexible since the effect of errors is amplified. When the cost is small, the model will “stiffen” and become less likely to over-fit (but more likely to underfit) because the contribution of the squared parameters is proportionally large in the modified error function.
	*  So we suggest fixing a value for € and tuning over the other kernel parameters.