## *State of the Art Iterative Docking with Logistic Regression and Morgan Fingerprints*

Morgan Fingerprints: 
- most popular molecular fingerprint
- aka ECFP4
- describing molecules as finger prints where we  are encoding their structural characteristics as a vector
- used for fast similarity comparisons forming the basis for structure-activity relationship studies, virtual screening and construction chemical space maps 
- not suited for large molecules
- related to MinHashed fingerprint MHFP6
### Abstract
- The paper re-docks to a receptor and lactamase using parallelized compute to massively reduce computation time to find top-ranked ligands 
- uses baseline featurization to show logistic regression on Morgan fingerprints 
	- Morgan fingerprint encodes the atom groups of a chemical into a binary vector with length and radius as its two parameters
- docking requires [crystal structure of a protein](gaps_ideas#martin_2021#idea1) and score molecules using some model of interaction with the binding site 
### Introduction
- 1s per ligand in ZINC20, docking with UCSF DOCK would take 20 years according to Lyu at al.
- 15s per ligand on average and that would take >300 years according to Gorgulla et al
- faster docking campaigns will broaden participation in virtual screening and ligand discovery
- avoid brute-force search by using stats (surrogate models)
	- iterative screening in virtual screening 
	- active learning in machine learning
		- reductions in docking time are achieved using classical mechanics or artificial neural networks 
			- ex: Graff et al, used simulated analyses to show an order of magnitude reduction in the number of docking calculations using a dataset of ligands docked to AmpC beta lactamase 
			- used surrogate modeling: message-passing network that applies deep learning procedures directly to molecular graphs without featurization 
- This paper
	- reports performance of iterative screening using logistic regression on data from Lyu
	- docking score to hit rate is in percentiles to make classification easier
	- performance is used to optimize baseline featurization 
	- performs better than message-passing network 
	- performance is target dependent 
	- ultra large docking campaign done in 1-2 weeks
### Results
#### Binarizing docking scores by percentile 
- classifiers require a cut off to binarize ligands into high scoring and low scoring classes 
- validation data: experimental in vitro inhibition assays from Lyu et al
	- hit rate was binned instead of dockin scores
	- binning can lead to artifacts that depend on the bin size 
		-   Binning is a way to group a number of more or less continuous values into a smaller number of "bins"
- Figure 1. additive model fit to the validation data using a logit link function, without binding and using ligand ranks instead of raw docking scores. used as a ranking tool not for seeing the distribution of binding affinities 
- ***Hit rate: proportion of assays in which the screening compound was active*** 
#### Binary fingerprints have a wide range of performance 
- Figure 2. shows average precision of molecular fingerprints available in RDKit dependent on fingerprint size. best performing fingerprint is morgan_feat fingerprint and larger the fingerprint size, the better the performance. Authors suggest using fingerprints greater than 8192 for ML efforts
- including pharmacophoric featurization improved performance at smaller sizes 
#### Proper sampling requires at least 400,000 ligands
- iterative docking relies on random sample as a training set
- training set must completely sample the chemical diversity in the high-scoring class such that it resembles the test set 
- training set should have good estimate of cut off percentile 
- relationship between predictive performance and training set size might gauge the range of best performance 
#### AmpC and D4: Single-iteration performance 
- enrichment: fold reduction in time compared to random search 
- enrichment and time spent docking are a function of model performance 
#### Comparison to previous work 
- alternate to single iterations is active learning 
	- random forest, neural network or message-passing graph neural network to regress molecule structure against docking score 
	- Graff et al

### Discussion 
- alternate to brute force search is iterative docking 
- a surrogate model is trained on random sample to steer towards high-scoring ligands 
- using morgan fingerprints with pharmacacophoric features and logistic regression shows a 10-fold enrichment over brute force search 
- goal: to minimize implementation cost by using fast featurization and learning algorithms 