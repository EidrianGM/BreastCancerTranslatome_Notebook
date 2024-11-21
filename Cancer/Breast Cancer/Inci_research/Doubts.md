* Why do you use “calcNormFactors” and “voom” functions of edgeR (v.3.34.1) and limma (v.3.48.3) instead of DESeq2 pipeline?
* Why do you use two different R's package cola versions 2.10 and 2.19 ? and why for different things ?
* PAM50 classifications was only applied to Cohort 1?
* Have you considered studying also the Lehmann classification for TNBCtype, refined to TNBCtype-4? 
* About Figure 1. C. What we see there is the classification in breast cancer subtypes according to the two omics data, but the real distribution of samples clinical classification matches?
* Should sequencing biases be included in the multiple linear regression-approach to calculate per-gene translation for each patient (Figure 2. A-B)? 
* How did you decide that there are 4 gene modules that identify the different subgroups (Figure 3 A)? 
* What is considered the activity of a upstream regulator?
* Are really cell abundances controlled? Did you plot the predicted abundances in the heatmaps?
* Why directly correlating the 1st cohort classification with cohort 2 and cell lines instead of applying first the stratification workflow?  
* Does it makes sense to use anota2seqUtils in the total mRNA ? To compare background results versus translatome results in a per patient o subtype fashion?
* What does the red colour intensity means in Figure S4?
* Genes with increased translational efficiency ? Are these genes simply those with z-score > 1? 

## About IA_Script1

* About the initial data in annotation_bcVivo_allSeqs.txt and merged_gene_counts.txt ?
	* The number of samples described in Fig 1. B does not match with what is in these files:
		* 
* Where are the quality control steps before applying preprocess_data() ??
	* I actually did PCA and I removed samples that had no data for one library type or that switched the direction…
* In the samples passed to filterExtraSample in function preprocess_data(), there are a set of samples that have been removed?
	* Why?
	* What is it with M 445T and M 445 T samples ?
* Why are we applying voom normalization?''

## About /Data information


