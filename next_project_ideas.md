  
`# Project Template 
`## Data`

`## Big question`

`## Baseline approaches`

`## How do we know we’re doing it right`

`## Alternative approaches if it doesnt work`

# WIP
## DrugMap

### Data
- [DrugMap](https://www.biorxiv.org/content/10.1101/2023.10.20.563287v1)
- Cysteine ligandability varies across cancer cells
- changes in cysteine reactivity 
- Due to: Cell redox states, protein conformation changes, genetic mutations
- reactive electrophilic compounds and combining this information with comprehensive genomic characterization
- 416 cell lines rep 25 cancer subtypes (repped by ~18 cell lines)
- quantified 14,000+ cysteine containing peptides per cell line
- in total: 78,778 Cys across 23,016 protein isoforms
	- 5999 cysteines are ligandable
- trained a feed forward convolutional neural network on structural parameters computed across 55,000+ human protein structures 
	- comes from PDB proteins that have cys
	- neural network has two components:
		- CNN (convolutional neural network) and MLP (multi-layered perceptron)
		- MLP input: tabularized biophysical calculations on cysteines plus corresponding cys liganding data from mass spec 
		- output: ligandability prediction 
Main Point: established the identity of cys in cancers that can be covalently targeted and provide a analytical platform to help id molecular and structural features underlying cys ligandability 
#### Method to collect the data
- isoTOP-ABBP with TMT
- cells are treated with cysteine reactive scout compounds-> cysteines form covalent adducts -> followed by pac-cysteine reactive probe (DBIA) which reacts with all remaining free cysteine thiolate groups
- DBIA will NOT tag cysteines that reacted with scout compounds 
- ligandable cystines == which are engaged by cysteine reactive compounds: e value > 60%
- for selecting scouts: mapped cysteines targeted by a larger set of 152 covalent frags
	- selected 3 scout proves that engage ~74% of cysteines covered 

#### Method to analyze cysteine ligandability
- they made a computational analysis 
	- CSEA (cysteine set enrichment analysis)
	- based on common gene-centric enrichment scoring algorithms 
	- instead of gene-level feature enrichment, CSEA determines enrichment signals at cys-level resolution
	- uses a repository of 6000+ cysteine sets compiled from molecular features, cysteine reactivity studies, reactivity changes, etc 

#### Cys ligandability findings
- microtubule-binding proteins are disproportionately ligandable 
- proteins that function as intramolecular scaffolds are enriched for cys ligandability in pancreatic cancers 
- proteins with CP type G domains are highly ligandable 
- EGF-JAK-STAT pathway is enriched across all cancel cell lines profiled and the Rho GTPase pathway is enriched in uterine cancers 
- alpha-helices have string enrichment of ligandable cys
- cystines that are highly solvent accessible or deeply burried are not favorable

#### Method to find redox score for each cell line
- give us insight into cancer cell redox states and protein conformational changes
- how does this affect cys ligandability?
- CSEA used to id molecular determinants governing heterogenous cys 
- increase expression of NRF2 (antioxidant regulator promotes reductive environment) increased cys ligandability 
### Questions Addressed in Paper
- KB03 scout showed greatest unique ligandability
	- so could we infer protein-structural correlates of cys liganding?
	- trained a feed forward convolutional neural network on structural parameters computed across 55,000+ human protein structures 
	- using 9000 cys in DrugMap that have corresponding structural annotations, they predict KB03 ligandability with ~70% accuracy 
- critical determinant of protein druggability: structural pocket available to accomadate small-molecule bidding 
	- pockets were identified using P2Rank and DeepPocket
	- deploy unique pocket segmentation strategies 
	- identified >250K high-confidence pockets across 55,500 protein structures 
	- ~5% ligandable cysteines lay within predicted pockets
	- cys in pockets are twice as likely to be ligandable (pockets have more leucine/aliphatic aa)
- differentially target proteins required for proliferation based on metabolic state of a cancer cell?
- can difference in liganding heterogenous cysteines function as a surrgoate readout for cellular redox states?
	- they computed proteomic redox scores for each cell line in DrugMap
- liganding of proteins can result in conformational changes 
	- hypothesized: covalent adduction of one cys in a protein might increase the accessibility to DBIA of another cys in protein (anti ligandable cys)
	- findings: emergence of a cryptic pocket upon inhibitor binding 
	- opening to study protein structural dynamics 
- how is cys ligandability influenced by cancer's genetic architecture?
	- applied hierarchical clustering to id genetic features ASSOCIATED with cys ligandability 
	- revealed three main clusters from multi-omics analysis 
- can we develop a probe to restrict transcription factor activity using DrugMap?
	- SOC10.C71 was targeted
#### Potential follow-ups by paper
- understanding differential responses to cys reactive drugs 
- this info can be leveraged to target proteins within cancers defined by a specific cell states in addition to targets characterized by mutation or differential expression 
- decipher how diff metabolic states can regulate cysteine ligandability 
	- important for designing new therapeutic strats
	- understanding which tumors may or may not be amenable to specific drugging approaches 
- molecular features underlying heterogeneity in cys ligandability
	- reveal role of conformational changes 
	- how cell states govern protein dynamics 
- many targets of interest have intrinsically disordered regions 
	- cys focused chemical proteomics: systematically maps sites of ligandability with covalent inhibitors 
	- cys anti-ligandability can serve as a proxy readout of protein conformational changes 
		- can be used to detec cryptic or transient pockets in mixtures of protein states 
		- mechanism for cys lacking annotated functions 
		- cysteine accessibility following engagement with drugs against EGFR and XPO1 an id an increase in ligandability among these structurally-sensitive cys 
- tumors have mutations of unknonw significance
	- functional consequences of mutation is unknown 
	- by using the genomic chracterization done in DrugMap
Main Point: understanding which cys is ligandable in cancer. chemical proteomics is a measure of protein-ligand interactions and hence conformational states. 
### Big Questions
- use their provided analytical platform to help id molecular and structural features underlying cys ligandability (under Data)
- Predict ligandability of anti ligandable cysteines after engagement with drugs using enrichment signal from CSEA? "enrichment" refers to the process of identifying whether a particular feature (such as a biological pathway or protein structural element) is overrepresented among a specific group of cysteines compared to what would be expected by chance.
- Predict warheads based on ligandability given in these models by perturbations to the three scout warhead types? we know that they interact w
- predict ligandibility of any cysteine in any protein using chemoproteomic data? 
	- can change based on redox states, protein conformation changes, genetic mutations, 
	- are the principles followed by ligandable and anti ligandable cysteines in cancer cell proteins the same as the ones in other proteins? studying the amino acid neighbors of ligandable cysteines?
	- https://chemrxiv.org/engage/chemrxiv/article-details/63edc76cfcfb27a31fdedfde (curated repo of cysteine chemoproteomics data-- identification, hyperractivity and ligandability of 24% of human proteome)
	- https://www.biorxiv.org/content/10.1101/2022.12.12.518491v1 (predicting accessibility of ligandable cystsines from chemoproteomics data)

- how different metabolic states can regulate cysteine ligandability?
### Baseline Approaches
### How do we know we're doing it right 

### Alternative Approaches






## Selectivity Predictions

How to use diff to predict selectivity (activity clefts—negative selectivity)

## Ensemble Docking 

## Diffusion
diffusion models for docking (add noise, denies a little, add noise, de-noise…) [**SE(3)-Stochastic Flow Matching for Protein Backbone Generation**](https://arxiv.org/abs/2310.02391)

[**Iterated Denoising Energy Matching for Sampling from Boltzmann Densities**](https://arxiv.org/abs/2402.06121)

**Use the diffusion to sample from MD ensemble** 

**Neuroplexer**

**Diff dock**

## Iterative Docking
For ladder: (ANI)

  

  

