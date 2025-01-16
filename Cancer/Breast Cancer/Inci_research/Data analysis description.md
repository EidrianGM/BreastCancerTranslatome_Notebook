Inci S. Aksoylu paper -> **Transcriptome-wide alterations in mRNA translation define breast cancer subtypes**

* Remove the RAMP sequence?
## Data source
* From: A.C. Camargo Cancer Center biobank (Sao Paulo, Brazil)
	* Two cohorts of primary non-treated breast cancer patients  (n=165)
		* I - 135 - all molecular sub-types
		* II - 30 - triple-negative 
## Methods
#### Experimental
* Polysome-profiling optimized for small samples
	* mRNAs associated to > 3 ribosomes
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
	* /home/sumosome/DB/refSeq/annotation/HUMAN/GCF_000001405.40_GRCh38.p14_genomic_chr_NM.gtf
	*  bamfiles <- dir(pattern='.bam$',path='.')
	* counts <- featureCounts(bamfiles, isPairedEnd = F,  annot.ext='/home/sumosome/DB/refSeq/annotation/HUMAN/GCF_000001405.40_GRCh38.p14_genomic_chr_NM.gtf', isGTFAnnotationFile=TRUE, GTF.featureType='exon', GTF.attrType='gene_id', ignoreDup=FALSE, useMetaFeatures=TRUE,countMultiMappingReads=FALSE,nthreads=8 )
	* Parameters: 
		* isPairedEnd = allowMultiOverlap = countMultiMappingReads = FALSE
* Filtering:
	* samples:
		* in case of only a sample total or polysome mRNA not passing the filter both mRNA data must be removed. Analysis is always paired total and polysome mRNA must be available for each sample after QC.
		* with fewer than 2.5 million reads
	* genes:
		* with 0 mapped RNA sequencing read in one or more samples 
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
		* CIBERSORTx in “absolute mode” using cell types signatures included in the built-in LM22 matrix and single cell signatures derived from human cell breast cancers. Specially immune cells and CAFs.
		* Still this not assures that the translation phenomena detected is found in cancer cells -> use of in vitro
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
	* Multivariate linear regression models application per gene and per replicate one sample at a time
		* What are the covariates here?
#### Analysis of gene signatures in patients and cell lines human breast cancer
* Link between alterations in mRNA translation and upstream regulators by: 
	* Empirical cumulative distribution functions
		* To test signatures in each patient, i.e. translationally regulated gene sets
		* Gene set activity is understood as the shift of residuals for each regulated gene set relative to background genes at the 50th quantile
		* The significance of the shift was determined using the Wilcoxon rank sum test
		* Activities in patient groups were asssesed by calculating mean per-gene residuals across patients within a subtype and then the shift and statistics relative to the background
#### Comparison of mRNA translation between patients and cancer cell lines

* Compare of translatome state in subtypes to cell lines:
	* cola::predict_classes (v.2.10.0, set.seed(123))
		* Parameters: 
			* nperm=100, dist_method=”correlation”
		* Data:
			* input is a scaled matrix prepared by calculating per-gene mean residual of 3 replicates from each triple-negative breast cancer cell line
				* ::scale (Parameters: center = F)
#### Identification of mRNA features associated with translation patterns in breast cancer subtypes

* Anota2seqUtils::featureIntegration
	* Input
		* per-gene mean residuals calculated across patients within a subtype
	* Three-step workflow:
		* Selection for each patients subgroup, two sets of 500 genes, the  most translationaly disregulated, most activated and most suppressed. 
		* These 1000 genes are tested for: 
			* 5’UTR features
				* GC content 
				* length 
				* G-quadruplexes (identified by pqs finder) 
				* presence of uORFs with strong Kozak context
				* presence of RBP-motifs annotated in ATtRACT database 
				* folding energy calculated by Mfold algorithm  
			* CDS features
				* codon usage
				* dicodon usage
				* amino-acid usage
	* EffScore and EffScore Adjusted calculation
		*  Measure the translation regulatory element effect

