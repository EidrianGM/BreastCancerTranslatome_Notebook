## Nature
* The 5’UTR is comprised of the cap-structure followed by a stretch of RNA-nucleotides until the start codon (AUG) of the **main ORF** and coding sequence
* Length 
	* Human median of 218nt, can reach up to 1200nt
* Composition
	* Modulated by alternative RNA splicing
	* Around 35% 5’UTR contain introns longer compared to those in coding regions
	* <label class="ob-comment" title="" style=""> Most eukaryotic mRNAs are mono-cistronic -> only one protein and lack upstream initiation site (uORF) <input type="checkbox"> <span style=""> According to Kozak </span></label>
* Transcription start sites (TSS) usage -> badly annotated
	* Differentially selected in response to altered cellular condition

## Scanning and initiation
### Scanning
* Unidirectionally 5’ to 3’ in the mRNA 
* Done by the 43S pre-initiation complex (43 PIC) 
* Until recognising the start codon AUG
* Kozak context
	* Strong -> the most favorable sequence for initiation
		* 5’-GCCGCC(A/G)CCAUGG-3’ (vetebrates)
		* Leaky scanning -> Bypassing the start codon
			* Mutations at the -3 position (A/G) relative to the AUG 
	* Weak -> non-canonical start-codons
		* Initiate at a frequency of 1-10% comparing
		* Codons AAG and AGG are non-functional 
		* Decoded by the leucyl-tRNA requiring eIF2A (instead of eIF2)
			* Loads antigenic precursors on major histocompatibility complexes 
* Start codon recognition 
	* Controlled by different eukaryotic initiation factors highly auto-regulated: 
		* eIF1
			* promotes scanning and inhibits recognition of non-AUG codons
			* harbors an AUG in weak context leading to increased eIF1 translation when eIF1 protein levels are low
		* eIF5
			* a GTPase-activating protein for eIF2 helps to dissociate eIF1
			* contains an inhibitory upstream open reading frame (uORF) in weak context
			* translated under low eIF1 conditions 
			* bypassed when eIF1 is high or eIF5 levels are low, leading to increased eIF5 levels
### Initiation
* Considered the rate limiting step in translation
* Length
	* Short 5’UTRs normally ≤20nt
		* Increased leaky scanning -> lower translational efficiency. Can result in N-terminal truncated proteins.
		* Mammalian mRNAs exception (TISUs):
			* The translation initiation of short UTRs (TISU) element
			* Promotes cap-dependent but scanning independent initiation
			* Found in mitochondrial related mRNAs and elements of the respiratory chain -> energy metabolism
			* Accepts 5’UTRs as short as 5nts 
			* Relies on specific sequences up and downstream of the AUG. downstream nucleotides compensate for lacking 5’UTR
			* eIF1 mediated
				*  Which normally prevents initiation at AUGs close to the cap
			* eIF4 mediated -> less on TISU integrity
				* A group of mRNAs with <50nts 5’UTRs  
				* Highly mTOR sensitive
	* Long


## Structures and sequence motifs
* Secondary structures formation
	* Longer 5’UTRs -> more structures and complex
		* Different requirements for translation initiation factors (eIFs)
		* Higher levels of **eIF4E** increase translation of mRNAs with higher structural content in the 5’UTR due to higher demand of **eIF4F** complex formation, involving RNA helicases like the ATP-dependent RNA helicase **eIF4A**
		* Particularly long 5'UTRs in yeast
			* Highly dependent on Ded1 (homolog of DDX3) and eIF4F dependent. eIF4F in yeast promotes translation initiation globally
	* Short 5’UTRs -> less structered
		* Lower dependency on eIF4A
		* More mTOR-dependen
	* GC content
		* Proximal to the 5’cap impede **eIF4F** complex formation
		* More dependent on RNA helicases DDX3 (DEAD-box family) and DHX29.
	* G-quadruplexes (RNA G4)
		* Common in oncogenic mRNAs 
		* Highly dependent on eIF4A, specially when co-varying with other structures such as hair-pin
		* Specific inhibitors for eIF4A as possible cancer treatment
* lncRNAs
	* Interactions 5’UTRs - lncRNA exist but rare
	* The murine Uchl1 mRNA is targeted by a lncRNA from the same locus leading to increased ribosome recruitment
	* Controlled by mTOR activity leading to increased cytoplasmic Uchl1 levels
	* Allows a bypass of cap-dependent translation utilizing an alternative initiation mechanism
		* eIF3 - bound to around 3% of all mRNAs
			* important role in the 43 PIC formation
			* recruited with a stem-loop in the 5'UTR
			* binds a hairpin in the 5’UTR of c-Jun, a regulator of proliferation, which when disrupted reduces eIF3-dependent translation
			* challenged by an internal ribosomal entry site (IRES) required for initiation by eIF3		
* Nutrient levels / Apoptotic processes
	* IRE - iron-responsive element
		* In the human ferritin 5’UTR. Forms a binding site for RNA binding proteins such as the Iron-responsive element-binding protein (IRP), when iron levels are low. Increased iron levels release IRP binding and induce translation of the iron storage protein ferritin.
	* IRES - internal ribosomal entry site
		* Specific 5’UTR sites in some viral mRNAs that by-pass the scanning mechanisms by recruiting the PIC. Approximately 10% of randomly selected mRNAs contain these structures.
		* Cap-independent initiation by IRES play an important role in adaptation to nutrient depletion in yeast
		* and when cells reprogram translation under apoptotic conditions, which leads to reduced global translation and a switch from cap-dependent to cap-independent initiation.
		* mediated by cleavage of the translation factors eIF4G, eIF4B and 4E-BPs by caspases and altered phosphorylation of 4E-BPs and eIF2α. 
		* In parallel rates of mRNA degradation increase and selective translation of pro-apoptotic factors is necessary. 
		* These specific apoptosis translational programs are initiated by IRES-mediated translation initiation and IRES trans-acting factors (ITAFs) These RNA binding proteins facilitate the assembly of initiation complexes independent of the canonical scanning mechanism mediated by eIF4F. Examples are hnRNPK stimulating c-MYC’s IRES-mediated translation and PTP binding the IRES of Apaf-1 and BiP.
## RNA modifications 

* Covalent bound of chemical groups, added by methyltransferases and removed by demethylases
* N$⁶$-methyladenosine (m$⁶$A)
	* stimulate translation, cap-independent but scanning-dependent utilizing eIF3. Similar role to the actual 5’cap for m$⁶$A.
	* Cellular stresses, i.e. heat shock, induce altered m$⁶$A patterns and translation inducing mediated by eIF3
	* Translation impaired due to impeded decoding of the CDS by tRNAs at m$⁶$A sites
* N$^1$-methyladenosine (m$¹$A)
	* Associated with increased initiation
	* And opposite conclusion
		 * m$¹$A are low abundant and regulate translation in a negative manner 
## uORFs - upstream open reading frames

* Upstream ORFs within the main ORF (above the first AUG-codon)
* Found in around 50% of transcripts most sites
* Evolutionary conserved
* Translatable due to ribosomes present in the initiation and elongation state
* The small peptides encoded are not well functionally characterized
* The detection of uORFs can underlie biases introduced by inhibitors of initiating and elongating ribosomes especially under stress conditions in which mRNA translation is limited
* Mechanism
	* Reducing initiation of main ORFs, especially when several uORFs are present
		* Represent protein levels alterations between 30-80% (in mouse)
		* However ribosome profiling show only a reduction of 15-30% translation
		* Mainly with AUG start-codons
	* Stronger repression
		* Within strong Kozak context
		* Longer distance between 5’cap and the uORF-AUG codon
			* More efficient initiation at uORFs while more robust scans the 43PIC
		* Shorter distance between the ORF and uORF
			* Reduced reinitiation potential could be observed using the pre-proinsulin mRNA in mouse, human and zebrafish, 
			* Depletion of uORF start-codons in favour of the main ORF
	* Lower repression
		* When the uORF recognition is moderately impaired, i.e. weak Kozak context
	* No substantial difference between 5’UTRs harboring an isolated uORF versus uORFs overlapping with the main ORF
	* Start codons
		* 25% AUG -> mainly inhibitory
		* 30% CUG
		* 41% variants: UUG, GUG, AGG, AACG, AAG, AUC, AUA, AUU
		* Yest cells exception:
			* Dramatic reshaping of transcription start sites and translation during meiosis involving initiation codons like UUG and CUG 
	* Terminating ribosomes at uORF stop codons can induce non-sense mediated decay, emphasizing the inhibitory potential of uORFs and connecting their regulatory potential to mRNA stability
* Genes which contain uORF have mechanisms well characterized:
	* The PIC initiates at the uORF AUG leading to increased translation of the uORF and subsequent lower translation of the main ORF
	* A peptide origination from the uORF stalling the 80S ribosome therefore acting as a roadblock to the scanning 43PIC, which did not initiate at the uORF AUG due to leaky-scanning.
		* Some inhibitory peptides functions as antizyme for the expression of different ornithine-decarboxylase homologs mediating polyamine-induced repression of the main-ORF, in which the start codon of their regulatory uORF is an AUU codon.
* eIF2 α subunit phosphorylation on Serine 51 
	* By four different kinases 
	* Regulates initiation resulting in global translation reduction and stress recovery
	* Results in lower GTPase-activity of eIF2B leading to decreased availability of functional ternary complexes
	* PIC proceeds to scan without available ternary complex resulting in increased leaky scanning on start codons, thus bypassing uAUG and promoting the main ORF under stress
	* Most transcripts encoding for genes with low susceptibility to stresses contain these uORFs leading to low translational efficiency of their main ORF in stress-free conditions
	* Transcripts without these uORFs underly stress induced reduction of global protein synthesis:
		* GADD34, regulatory subunit of the phosphatase PP1, exhibiting auto regulatory activity, which antagonizes eIF2α phosphorylation
		* ATF4, a transcription factor leading to induction of CHOP and GCN4, leading to cell death if stress conditions persist. Contains two major uORFs that modulate translation by initiating at a short uORF upstream of a second uORF which overlaps with the main ORF. The remaining ternary complex at the stop codon of this uORF, initiates after 60S dissociation at the overlapping uORF preventing translation of ATF4.
		* GCN4 in yeast, is activated by GCN2 upon amino acid starvation. Here four uORFs regulate the translation of the main ORF, demonstrating the same phenomena as in ATF4 when the remaining 40S subunits reinitiate with ternary complexes at the three following uORFs. This reinitiation is limited when pospho-eIF2α levels are high, 43S PICs resume leaky scanning leading to recognition of the GCN4 start-codon 
		* eIF3
			* Plays a role in reinitiation after short uORFs by interacting with structures in the 5’UTR in the case of GCN4 and ATF4 mRNAs. Additional factors like DENR and MCT-1 are necessary for reinitiation after longer uORFs
	* Implicated in different neurological conditions and liver development.
	* Loss of Gcn2 in mice and a subsequent decrease in phospho-eIF2α to reduce translation of ATF4 mRNA is leading to increased memory
* The mutation of the uAUG in the CCAAT/enhancer-binding protein beta (C/EBPβ) impairs liver development in mice, herein by dysregulating the translation of different N-terminal isoforms of C/EBPβ 

## TOP mRNAs
* mRNAs harboring a C-residue at the cap-site followed by a stretch of 4-15 pyrimidines, called “terminal oligo pyrimidine tract” - TOP
* The C at the cap-site and/or the replacement of the following base to an A abolishes TOP-functionality
* Relying on the integrity and composition of the TOP-motif
* Conserved among vertebrates and in the ribosomal proteins in Drosophila melanogaster, however not in yeast and neither in Caenorhabditis elegans 
* Highest expressed and dominated by 80 ribosomal proteins with a smaller proportion of 5 eukaryotic elongation factors (eEFs) and 2 eukaryotic initiation factors (eFIs)
* Probably more mRNAs harbor a TOP-motif
*  Function as a cis-regulatory element 
* “All-or-nothing”-mechanism
	* TOP mRNAs switch between extremely efficient translated under normal growth conditions to largely repressed under cellular stress
	* Around 30% of TOP-mRNAs remain translationally repressed in optimal growth conditions
	* Explained because ribosome production and maintenance of the protein-synthesis machinery is extreme energy consuming. Cells can therefore tune the production of protein synthesis components in a dramatic and efficient manner. Indeed, unfavorable growth conditions, such as serum starvation or contact inhibition, will cease TOP-mRNA translation.
	* PI3K-AKT pathway to signal transduction regulating TOP-mRNA
	* Requires TSC1/2 and their downstream target, the GTPase Rheb
	* TOP-mRNA translation is highly dependent on activity of mTORC1
	* The depletion of amino acids leads to mTORC1 inactivation, reduced activity of S6K and rpS6 phosphorylation. However, alterations of S6K and P-rpS6 do not impact TOP-mRNA translation
	* 4E-BPs play a major role in regulating TOP-mRNAs
		* Mouse embryonic fibroblasts lacking 4E-BPs exhibited less repression on TOP-mRNA translation upon inhibition with mTOR inhibitors such as Torin1 and INK128.
		* Other TOP-mRNAs are shown un-sensitive to eIF4E
		* Stimuli like oxygen, nutrients and growth factors alter TOP mRNA-translation in an mTOR dependent but 4E-BP-independent manner  suggesting another mechanism of mTOR not involving 4E-BPs. 
	* TIA-1 and TIAR, factors associated with stress granules, regulate translation of TOP-mRNAs depending on amino acid level mediated by GCN2 and activation of mTOR
	* La-related proteins (LARP) show TOP mRNA translation regulation
		* LARP1, phosphorylated by mTORC1 upon association with raptor interacts with the TOP motif via its DM15 domain regulating translation and mRNA stability of TOP-mRNAs.
		* LARP1 also interacts with the 5’cap of TOP-mRNAs proposing a competitive effect with eIF4E impeding the assembly of the eIF4F complex
		* The cap binding of LARP is mediated by mTORC1, although it is debated if LARP1 acts as a repressor or activator of TOP-mRNA translation. 
		* Surely repress translation downstream of mTORC1
		* But an activating role is suggesting a context dependent effect
		* LARP1 binds the 5’cap and PABP and associates with polysomes in a mTOR-dependent manner
		* LARP1 plays a role in TOP-mRNA stability

