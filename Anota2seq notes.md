* Anota2seq cannot use data from competitive two channel experiments when the polysome-associated mRNA is directly compared to total mRNA as these do not allow independent estimates of polysome-associated mRNA and total mRNA levels1.
* anota2seq requires 3 replicate experiments per group if there are 2 conditions
*  Analysis of Partial Variance (APV) = statistical framework
	* feature-based (gene-based) regression to control spurious correlations leading to elevated false positive findings
		* On opposite to studies of changes in translational efficiency commonly applied per sample differences (log scale) between levels of translated mRNA and total mRNA among two or more conditions
	* **APV analysis produces residuals that are uncorrelated with the total mRNA levels and identifies changes in translational efficiency leading to altered protein levels or buffering**
	* Requires filtering of features/genes: 
		* with 0 counts in any sample
		* Without variance in any mRNA source
### QC
* In the QC if a similar number violations as expected by chance occur, it is assumed that anota2seq can be applied.
* **Highly influential datapoints**
	* Attempts to establish if there are more influential data points compared to what would be expected by chance when considering all analyzed features
	* Calulates the **standardized dfbeta** for the slope of the regression and several thresholds to determine whether or not a data point is highly influential
# Doubts
* The statement "***if a similar number violations as expected by chance occur, it is assumed that anota2seq can be applied***" 
	* It means that data should not show more violations than random data ?
* **standardized dfbeta**
	* How is this method compared to penalised models?


# Weird Code Things
* Function: anota2seqPerformQC()
* The if in line 129 is never tested see:
    groupSlopeP[i] <- 1
    if (groupSlope[i] > 1 | groupSlope[i] < 0) {
      groupSlopeP[i] <- anota2seqSlopeTest(tmpLm = tmpLm, 
        curSlope = groupSlope[i], "translation")
    }
