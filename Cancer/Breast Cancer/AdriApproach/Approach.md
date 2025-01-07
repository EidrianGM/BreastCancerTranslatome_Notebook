
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
	* Polysome associated mRNA abundance - gene level (PREFERRED BY OLA)
		* Continuous value.
			* Distribution?
				* Symmetric 
				* Skewed
		* Relationship between the number of samples (n) and number of predictors (P)
			* Samples here are the genes and predictors are clinical and cell types variables associated to patient
				* Here there are more Samples (genes) than predictors. 
					* Although LMs are initially fitted to each gene individually... this is weird. This actually causes to have more predictors than samples.
	* Molecular classification of Breast Cancer - patient level
		* Categorical value:
			* HER2
			* Luminal A
			* Luminal B
			* Triple Negative or Basal
		* Distribution?
				* Balanced
				* Unbalanced -> Clearly is this one
		* Relationship between the number of samples (n) and number of predictors (P)
			* Samples here are the patients and predictors are the genes values + clinical and cell types variables associated to each patient
				* Here there are more predictors (coding genes and variables) than samples. 
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
* Summary Table

| **Characteristic**      | Data set          |                                 |
| ----------------------- | ----------------- | ------------------------------- |
| **Dimensions**          |                   |                                 |
| Samples                 |                   |                                 |
| Predictors              |                   |                                 |
|                         |                   |                                 |
| **Response variable**   | **Polysome mRNA** | **BC Molecular Classification** |
| Type (Categ. or Cont.)  | Continuous        | Categorical                     |
| Balanced/Symmetric      | ?                 | ?                               |
| Unbalanced/Skewed       | ?                 | ?                               |
| Independet              | ?                 | ?                               |
|                         |                   |                                 |
| **Predictor variables** |                   |                                 |
| Continous               | X                 | X                               |
| Categorical             | X                 | X                               |
| Count                   | X                 |                                 |
| Correlated/Associated   | X                 |                                 |
| Different Scales        | X                 |                                 |
| Missing Values          |                   |                                 |
| Sparse                  | ?                 |                                 |
