1. Come up with total mrna markers of the translation subtypes. Feature selection.
	* I used logistic regression, then elastic net etc. And also random forest but the models didnt really work out. Because we have some small clusters n=6 as well.. So ola wanted you to regress my residuals to the total mrna amount for each group and gene. And the ones that correlate the best might be our ideal biomatkers.
	* TRIED:
		* elastic_net
		* lasso
		* random forest
	* TO USE:
		* support vector machines