
Steps:
0. Optional preprocessing steps of pathway database 
	* dissectDB() ->  make more granular the pathways database
		* Better to use it by deffault
		* Mathematically, it checks for genes variance in the pathway, if there is, it gets splitted  	
	* diseasePaths() -> select important paths
1. Get scores -> get pathways scores  
	* getScores() -> scores matrix by sample and important paths
		* Depends on
			* DB and Score
				* M-Score -> z-score average
					* Requieres the gene sets annotations / pathway to be co-expressed or use dissectDB()
					* Not influenced by sample size
				* GSVA
					* It might do no require dissectDB()
					* Influenced by sample size and missing value
					* Better to integrate different datasets
				* Rank based -> not reccommended
					* SSGSEA and Sign Score
						* Fail with activators and inhibitor genes, better use dissectDB()
2. Perform clustering
3. Apply machine learning
	* getML()


