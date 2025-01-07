
## Objective 
- Train a model to obtain the residuals able to explain the variance of polysome mRNA according to the cytosolic mRNA
	- After proper preprocessing and quality control
		- Robust samples
			- > 2.5M reads
			- Good PCA classification
			- Different samples in cohort 1 and 2
			- Enough genes coverage
		- Robust genes
			- With reads in a high % of samples or in all 
			- Only coding genes
- Use the residuals to stratify breast cancer patients
## Methodology
Depends greatly on the type of data
#### Data description
* Response variables
	* Polysome associated mRNA abundance
		* Continuous value
			* Which distribution?
				* Symmetric 
				* Skewed
	* Molecular classification of Breast Cancer
		* Categorical value
			* HER2
			* Luminal A
			* Luminal B
			* Triple Negative or Basal
			* Distribution?
				* Balanced
				* Unbalanced -> Clearly is this one
* Predictors
	* Library sizes = total reads 
		* in polysome
		* in cytosol
	* Cell types abundance (CIBERSORTX)
		* Inmune cells 
		* Atlas cells
		* WARNING: 
			* training the model with two CIBERSORTX runs introduces noise because is like saying a sample has two different distribution of cell types, I mean a sample cannot have 60% of B cells and 50% of Normal Epithelial.
	* Clinical features