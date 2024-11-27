- If the residuals extraction comes from a simple linear model or is RVM, in the polysome vs total?

All seems to be done with lm or anova::lm

1. We first run a univariate analysis using the abundances of each of these cell lines to understand whether they have an influence on mRNA translation. Any cell line that has a significant effect in the univariate model is later included in a multivariate model. 
	models_prerun <- lapply(colnames(dfWithExp)[-c(1,2,3,4)], function(x) {
      anova(lm(substitute(ExpPoly ~ LibSizePoly+LibSizeTot+ExpTot+j, list(j = as.name(x))), data = dfWithExp))
    })
2. Select any cell lines that have any genes with FDR < 0.15 and perform stepwise regression
	initialFormula <- lm(ExpPoly~LibSizePoly+LibSizeTot+ExpTot,data=dfWithExp)
	       updated_formula_str <- paste("ExpPoly ~ LibSizePoly + LibSizeTot + ExpTot +", paste(c(attr(initialFormula, "variables"), new_term), collapse = " + "))
      storeModels[[j-3]] <- anova(lm(as.formula(updated_formula_str),data=dfWithExp))}
3. Same process repeated for clinical parameters. First the univariate analysis and then the multivariate analysis to identify the clinical parameters to be included in the final analysis. 
      anova(lm(substitute(ExpPoly ~ LibSizePoly+LibSizeTot+ExpTot+T_cells_CD8+T_cells_CD4_memory_resting+T_cells_CD4_memory_activated+Treg+Macrophages_M2+Mast_cells_activated+Eosinophils+Plasmablasts+CAFs+j, list(j = as.name(x))), data = dfWithExp))})
4. Now run multivariate model, stepwise regression.. 
		    colnames(dfWithExp) <-c("ExpPoly","ExpTot","LibSizeTot","LibSizePoly",colnames(annot_T[,selectFeature_CellTypesFinal]),colnames(annot_T[,selectFeature]))
    initialFormula <- lm(ExpPoly~LibSizePoly+LibSizeTot+ExpTot+T_cells_CD8+T_cells_CD4_memory_resting+T_cells_CD4_memory_activated+Treg+Macrophages_M2+Mast_cells_activated+Eosinophils+Plasmablasts+CAFs,data=dfWithExp)
    for(j in c(14:(ncol(dfWithExp))-1)){
       new_term <- colnames(dfWithExp)[13:j + 1]
       # We see that the cells lines such as CD8 T Cells, Resting and Activated CD4 Memory T cells, T-Regs, M2 Macrophages, Activated Mast Cells, Eosinophils, Plasmablasts and CAFs have an influence on mRNA translation therefore we include these to the model as well. 
       updated_formula_str <- paste("ExpPoly ~ LibSizePoly + LibSizeTot + ExpTot + T_cells_CD8 + T_cells_CD4_memory_resting + T_cells_CD4_memory_activated + Treg + Macrophages_M2 + Mast_cells_activated + Eosinophils + Plasmablasts + CAFs +", paste(c(attr(initialFormula, "variables"), new_term), collapse = " + "))
      storeModels[[j-12]] <- anova(lm(as.formula(updated_formula_str),data=dfWithExp))
      }
    lmTmp <- lm(ExpPoly~LibSizePoly+LibSizeTot+T_cells_CD8+T_cells_CD4_memory_resting+T_cells_CD4_memory_activated+Treg+Macrophages_M2+Mast_cells_activated+Eosinophils+Plasmablasts+CAFs+Histological_grade+Necrosis+family_history_cancer+ExpTot,data=dfWithExp)

lm -> fit linear models, including multivariate ones. 
* applied with default settings
* lm(formula, data, subset, weights, na.action,
   method = "qr", model = TRUE, x = FALSE, y = FALSE, qr = TRUE,
   singular.ok = TRUE, contrasts = NULL, offset, ...)