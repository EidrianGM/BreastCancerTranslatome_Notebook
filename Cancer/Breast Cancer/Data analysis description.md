Inci S. Aksoylu paper -> **Transcriptome-wide alterations in mRNA translation define breast cancer subtypes**

## Data source
* From: A.C. Camargo Cancer Center biobank (Sao Paulo, Brazil)
	* Two cohorts of breast cancer patients (n=165)
		* I - 135
		* II - 30
## Methods
#### Experimental
* Polysome-profiling optimized for small samples 
* Single-end libraries prepared following the Smart-Seq2 protocol
	* Illumina HiSeq2500
		* 50 base single-end reads
#### RNA-seq
* QC
	* Trimming using BBMap (v.36.69)
		* Nextera and Truseq adapters
		* Ribosomal RNA 
		* Paramenters:
			* k=13, ktrim=n, useshortkmers=t, mink=5, qtrim=t, trimq=10, minlength=25 and rRNA reference sequences from SILVA db
	* Alignment:
		* HISAT 2 v.2.1.0 with default settings for single-end
		* To human reference genome hg38
#### Expression Matrix Analysis
* featureCounts with Rsubread v.2.6.4; p
	* Parameters: 
		* isPairedEnd = allowMultiOverlap = countMultiMappingReads = FALSE
* Filtering:
	* samples with fewer than 2.5 million reads
	* genes with 0 mapped RNA sequencing read in one or more samples 
* Counts normalization:
	* TMM-Log2 by “calcNormFactors” and “voom” functions of edgeR (v.3.34.1) and limma (v.3.48.3)
* PCA on TMM-Log2 counts:
	* PCAtools::biplot (parameters: removeVar = 0.75 and scale = T)
	* Removed outlier samples -> final matrix 
#### Stratification / Subtyping / Classification

* PAM50 panel 
	* genefu::molecular.subytping (v.2.24.2) 
		* Parameters: 
			* sbt.model=”pam50”, data = normalized counts for either total or polysomal mRNA, annot= annotation for each sample
#### Translatome modelling
* Linear regression models correlating total cytosolic and polysome-associated mRNA levels
* Removal of confounding factors
	* Cell composition
		* CIBERSORTx in “absolute mode” using cell types signatures included in the built-in LM22 matrix and single cell signatures derived from human cell breast cancers
	* Clinical variables
	* Univariate and multivariate regression models
		* To identify the significant associations between confounding factors and alterations in polysome mRNA levels
		* Per gene and per patient residuals and slopes were collected from a final multivariate linear regression model corrected for:
			* <label class="ob-comment" title="" style=""> library sizes <input type="checkbox"> <span style=""> average read lenght? total number of reads? total expression? </span></label>
			* cell types
			* clinical covariates
#### Sample classification per-gene and across-patient translational efficiencies

* Starts with residuals from previous multivariate linear regression models
* Using cola package(v.2.10.0)
* Optimal clusters identification
	* ::run_all_consensus_partition_methods 
		* Parameters:
			* kmax=10 
	* ::select_partition_number
		* Results -> k=6   
		* ATC and mclust combinations
			* evidenced by mean silhouette, concordance, Jaccard index and 1-PAC values
* Clustering
	* ::consensus_partition (set.seed(1233))
		* Parameters
			* top_value_method= "TC", partition_method="mclust", max_k = 10, partition_repeat = 100
	* Heatmap visualization
		* ::get_signatures
			* Parameters
				* k=6, silhouette=0.75, group_diff = log2(1.5), fdr_cutoff=0.01
* Enrichment Analyses
	* ::enrichGO 
		* Parameters
			* orgDb= org.Hs.eg.db, keyType=“ENSEMBL”, ont=”BP”, pAdjustMethod=”BH”, pvalueCutoff=0.01, qvalueCutoff=0.01
#### Triple-negative breast cancer cell lines translatome
* 6 cell lines starved for 16 hours
* Expression analysis:
	* Affymetrix GeneChip Human Transcriptome Array 2.0 (HTA 2.0)
	* Normalisation
		* affy::rma (v.1.70.0)
		* log2-transformation -> biobase::exprs
	* Multivariate linear regression models application
		* What are the covariates here?
	* 