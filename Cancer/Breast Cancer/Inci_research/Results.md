## Quantification of mRNA translation in breast cancer patients

* Total mRNA perfectly classify according to PAM50 classification
* Polysomal mRNA fails to group together samples according to PAM50

## Abundant variation in mRNA translation across breast cancer patients

* I don't really understand how this analysis is carried out, but it basically consist in two steps:
	1. Adjust input matrix to all possible covariates:
		* Cell populations abundance
		* Clinical variables
		* Sequencing biases ?
			* Library Size:
				* Total reads ?
				* Total unique reads ?
				* Average read length ?
	 2. Measure how many genes are translationally dysregulated.
* Results: Many genes are translationally dysregulated

## Transcriptome-wide alterations in mRNA translation define breast cancer subtypes

* There are 6 subtypes of shared patterns of rewired mRNA translation across breast cancer patients
	* These appeared to be distinct from PAM50 subtypes
	* Their clinical annotations does not define them
* These subtypes can be divided according to 4 different gene sets
* The 6 subtypes are also found in the second cohort of TNBC validating the subtypes.

## Upstream regulators of mRNA translation associate with translation in breast

* Association of translation regulation mechanisms per patient subtypes 
	*  mTOR singaling pathway
	* activity of subunits of eIF4F complex
	* cellular stress
	* DAP5-dependent translation
	* U34-modifications
	* ECM
## In vitro models of TNBC recapitulate translation subtypes

* In order to discard that subtypes originate from non-cancer cells
* Find cancer cell lines to mirror the subtypes 
*  Polysome-profiling in 6 triple-negative breast cell lines:
	* HCC1937 -> Subtype 4
	* MB157 -> Subtype 1
	* MB468 -> Subtype 2
	* ?
	* ?
	* ?
* TNBC cell lines can be used to study mechanisms underlying translation patterns

## Cis- and trans-acting factors associate with altered mRNA translation in breast cancer subtypes

* anota2seqUtils results:
	* All subtypes had an indispensable effect exerted by the codon composition of the CDS. Codon usage may drive the heterogeneity in translational landscape of breast cancer.
		* Subtype 2 genes with decreased translational efficiency are enriched on AAT
		* Subtype 3 genes with increased translational efficiency are enriched in AAT 
	* Trans-acting factor on subtypes with step-wise linear regression analysis 
		*  40% variance explained in cis-acting features = mRNA features alone
		* 45% variance explained in downstream signatures of trans-acting features -> additional pathways are active