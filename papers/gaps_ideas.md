gaps can mean gaps in knowledge identified by the paper, by me, by anyone else. 
ideas can mean thoughts, opinions, and ideas about exploring future questions. 

## [[pogorzelska_2018]]: 
#### gap1
in mammals: lysosomal cathepsins. 11 identified in humans (B, C, F, H, L, K, O, S, V,  X, W)
structures solved for everything except lysosomal cathepsins O and W

#### idea1
find a way to take out mannose-6-phosphate moiety recognition marker to stop binding to receptor in Golgi and hence stop transportation to lysosomes 

#### idea2 
maybe we can artificially control acidic conditions to activate the inactive protein (generally known as zymogen) or deactivate the protein to control its lysosomal protease activity 

#### idea3
inhibition of autocatalysis or transactivation can maybe prevent activation of CTPs in lysosomes

#### idea4
need to be wary of how much we are inhibiting CTPs with natural or artificial inhibitors. what experimental studies can we do to find out what the sweet spot is to inhibit CTPs but not cause a deficiency? 

#### idea5
inhibitors can be modeled with cystatin C in mind. enzyme-cystatin interaction is not a simple reaction with the catalytic cysteine residue of the cysteine protease. the interaction relies on hydrophobic contacts between the binding regions of cystain and binding pockets of the enzyme. cystatins do not react with the catalytic center which is what we may want from potential therapeutics 

#### idea6 
stefin A/B and other cathepsins are found to be deregulated in tumors, promoting expression of CTPs which are known to help in dissemination of cancer cells. therapeutics that may promote a higher expression of stefin A/B or other cathepsins could be another way to repress expression of CTPs in a controlled manner. 
Studies show that Stefins A and B were up regulated in lung tumors and were able to neutralize harmful tumor-associated proteolytic activity 

#### idea7
can try to develop therapeutics that target cells with cancer markers only in order to inhibit CTPs involved only in cancer cells
authors suggest designing allosteric inhibitors that bind outside the AS of enzymes (in the cavity lacking a physiological role)
authors also suggest dev of SiRNA drugs that are highly specific and efficient in silencing of a target gene-- issue is with precise and systematic delivery 

## bender_2021
### idea1
the first step to drug discovery, computationally, can always be large scale docking of millions of ligands to a given protein. This will help eliminate anything that doesn't have any chance of binding to the protein as quickly as possible (including accessibility screens, etc). The next step would be to improve resolution of the docking simulations for ligands that pass first screen. This will again prioritize ones that have a better chance of binding. This second screen could involve using something like autodock vina and the final screen can include FEP calculations to really narrow down our list of ligands for a given protein. 
[DOCK3.7 paper](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0075992)
AutoDock Vina is a program for molecular docking and virtual screening. It uses a gradient optimization method to predict the preferred orientations of a ligand molecule bound to a protein. It uses a united-atom scoring function (amber force field). grid-based energy approach with a genetic algorithm to sample poses. 
	DOCK focuses on physics-based scoring functions with few terms and sampling by graph-matching between ligand atoms and receptor 'hot-spots'. Two branches of DOCKx.x: 
		DOCK6.x focuses on accurate prediction of ligand geometries and adopts a wider range of scoring functions (making it more accurate but slower?). hot-spot-based graph matching focused the search for complementary ligand orientations to the protein. 
		DOCK3.x have physics-based scoring functions with few terms to be optimized for speed needed for huge library screen. it uses a flexibase of pre-calculated ligand conformations-- so it doesn't need to search/build for conformations every time something needs to be docked. 
		
### idea2
can use the protein structure/function pipeline here maybe 
how to incorporate the ligand during modeling?
