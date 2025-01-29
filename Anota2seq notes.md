* Anota2seq cannot use data from competitive two channel experiments when the polysome-associated mRNA is directly compared to total mRNA as these do not allow independent estimates of polysome-associated mRNA and total mRNA levels1.
* anota2seq requires 3 replicate experiments per group if there are 2 conditions
*  **Analysis of Partial Variance (APV) = statistical framework**
	* feature-based (gene-based) regression to control spurious correlations leading to elevated false positive findings
		* On opposite to studies of changes in translational efficiency commonly applied per sample differences (log scale) between levels of translated mRNA and total mRNA among two or more conditions
	* **APV analysis produces residuals that are uncorrelated with the total mRNA levels and identifies changes in translational efficiency leading to altered protein levels or buffering**
	* Requires filtering of features/genes: 
		* with 0 counts in any sample
		* Without variance in any mRNA source
	* APV assumes that the slopes of the regressions from each individual condition are the same such that using the common slope is valid.
### QC
* In the QC if a similar number violations as expected by chance occur, it is assumed that anota2seq can be applied.
* **Highly influential datapoints**
	* Attempts to establish if there are more influential data points compared to what would be expected by chance when considering all analyzed features
	* Calulates the **standardized dfbeta** for the slope of the regression and several thresholds to determine whether or not a data point is highly influential
* **Common slopes between treatment groups**
	* APV assumes that the slopes of the regressions from each individual condition are the same such that using the common slope is valid. This assumption postulates that the relationship between the translated mRNA level and the total mRNA level shows the same slope for each condition
	* We expect that a number of interactions with low p-values will arise simply due to chance also when true positive interactions are absent
	* If the number of interactions does not exceed what is expected by chance, **their p-values should follow a uniform distribution and anota2seq can be applied using common slopes for all features**
* **Normal distribution of regression residuals**
	* Assesses whether the residuals from the linear regressions (feature by feature) of translated mRNA level to total mRNA level are normally distributed by generating normal Q-Q plots of the residual.
	* If the residuals are normally distributed, the data quantiles will form a straight diagonal line from bot tom left to top right. If the resulting residuals deviate strongly from normality an alternative normalization method could be tested.
	* If there are 99 samplings we expect that 1/100 values should be outside the range obtained from the samplings. Thus it is possible to assess if approximately the expected number of outlier residuals are obtained.
	* If approximately the expected number of outlier residuals are observed, the data set is suitable for anota2seq analysis
# Doubts
* The statement "***if a similar number violations as expected by chance occur, it is assumed that anota2seq can be applied***" 
	* It means that data should not show more violations than random data ?
* **Standardized dfbeta**
	* How is this method compared to penalised models?
* **APV assumes that the slopes of the regressions from each individual condition are the same such that using the common slope is valid.**
	* i.e., condition and total mRNA levels do not interact in predicting translated mRNA levels ?
	* Is this to remove the effect of the condition?
	* Assuming the same slope for controls and treatment is not the same as saying that translation regulation mechanisms do not depend on condition/perturbations/stimulli?

# Weird Code Things
* Function: anota2seqPerformQC()
* The if in line 129 is never tested see:
    groupSlopeP[i] <- 1
    if (groupSlope[i] > 1 | groupSlope[i] < 0) {
      groupSlopeP[i] <- anota2seqSlopeTest(tmpLm = tmpLm, 
        curSlope = groupSlope[i], "translation")
    }
* In featureIntegration() -> resQuant(qvec = a2sU_eff(a2sU), a2sU = a2sU)
	* qvec = a2sU_eff(a2sU) -> gets THE translation.apvEff from SafeQuantResults
	* Why ?? What is it for qvec ?
	* resOut <- resQuant(qvec = a2sU_eff(a2sU), a2sU = a2sU) 
		* resOut -> translation.apvEff divided in background and translation directions up / down ? Why not buffering ?
* Functions without documentation ?
	* prepFeatures
	* a2sU_features
	* a2sU_eff
	* resQuant
	* checklmfeatGroup
	* checklmfeatGroupColour
	* 
## Improvements
Here I will put examples of things that are not strict errors but that can be actually worth controlling just for the sake of making anota2seq and postnet more user-friendly
* anota2seqPerformQC()
> 	ads <- anota2seqPerformQC(Anota2seqDataSet = ads, generateSingleGenePlots = TRUE, fileName = "singleReg.pdf", fileStem = pasfiguresFolder)
	  |--------| 100% Error: object 'pasfiguresFolder' not found
* Control first that fileStem variable exists...


I don't understand how comparisons works in featureIntegration.
The documentation of ?featureIntegration states:
`comparisons`  - Relevant for linear model only (analysis_type="lm") and if regulated genes are only considered (regOnly=TRUE). Indicate which regulation/geneList pairs should be compared. It should be provided as a list of vectors with pairs of indexes in regulation/geneList (for example list(c(0,2),c(2,4)) would indicate that the background (0) would be compared to the second and the second to the fourth mode of regulation/geneList. If both regulation and geneList are provided, geneList is appended to the end.

okey so 
0 is always all the genes in a2sU as provided by resOut <- resQuant(qvec = a2sU_eff(a2sU), a2sU = a2sU)

but what are 1, 2, 3, 4, 5 ?

If I do comparisons = list(c(1,2))
1 is translationUp_c1
2 is translationDown_c1

If I do comparisons = list(c(3,4))
coloursTmp <- c("grey75", coloursTmp)[compTmp]
<NA> <NA> 
  NA   NA
listSel <- c(names(resOut[[compTmp[1]]]), names(resOut[[compTmp[2]]]))
Error in resOut[[compTmp[1]]] : subscript out of bounds

I thinks this is happening simply because for my anota2seq results 
resOut <- resQuant(qvec = a2sU_eff(a2sU), a2sU = a2sU)

is only returning 
> names(resOut)
[1] "background"         "translationUp_c1"   "translationDown_c1"

If I do comparisons = list(c(0,2))
0 is background
2 is translationDown





be compared to the second and the second to the fourth mode of regulation/geneList

