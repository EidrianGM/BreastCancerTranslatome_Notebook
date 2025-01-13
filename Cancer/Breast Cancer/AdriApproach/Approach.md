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
| Model type              | Regression        | Classification                  |
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
## 3. Methodology steps
### 3.1. Pre-processing the predictor data
### 3.2. Estimating model parameters
### 3.3. Selecting predictors for the model
### 3.4. Evaluating model performance
### 3.5. Fine tuning class prediction rules (via ROC curves, etc.)

## 4. Identification of Translation Dysregulated Genes
* By Slope
From the linear model we select genes which have an slope between 1 and 0, that is inversely correlated with the translation dysregulation. This is the close to 0 slope the more associated to translation regulation. Conversely the close to 1, the most coordinated changes between transcription and translation thus no dysregulation process is taking place.
* By R2
	* The model R2, which explain how well the polysome mRNA is explained by the different predictor variables, should have values ????
* Gold Standard
	* There should be a set of genes that can act as gold standard of coordinated changes, for example the PAM50 genes that are able to classify breast cancer patients based on transcriptome and proteome.

