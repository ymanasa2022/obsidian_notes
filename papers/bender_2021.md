## *A Practical Guide to Large-Scale Docking* 

### Abstract 
- structure-based docking screens of large compound libraries
- establishing controls to avoid under sampling of configs is important 
- paper shows procedure to evaluate docking parameter for melatonin receptor
- uses DOCK3.7 

### Introduction
- DNA-encoded libraries: collection of small molecules linked to DNA that contains unique information about the identity and structure of each molecule. The DNA tags, or "bar codes", record the synthetic history of each molecule
- DNA encoded libraries are limited to aqueous solutions thus limiting chemical rxns and chemical libraries 
- 'make on demand' libraries: Enamine 
- structure based molecular docking: simulations of docking many ligands to a protein 
- large scale docking is unable to simulate enough interaction terms to achieve chemical accuracy
- they only help eliminate molecules that are definitely unable to bind a target, [prioritizing ones that have a change](gaps_ideas.md#bender_2021#idea1)

### Large library docking workflow

![[large_docking_workflow.png]]
##### Structure Prep
- high resolution ligand-bound structure outperform ligand-free structures 
	- tools like SphGen, SiteMAp and FTMao can be used to identify potential ligand binding sites 
- small enclosed binding pockets perform better than flat and solvent-exposed binding sites which are typical of ppi 
- mutations in high res structures should be reverted to wild type (missing side chains and loops should also be added)
- can include water molecules. treat them as non-displaceable parts of the protein structure. include them esp water molecules are enclosed in the targeted binding pocket 
- buffer components should be removed
- hydrogen atoms should be removed and remodeled. Hydrogens part of certain residues can be modeled using programs like Reduce (included in DOCK3.7), Maestro, ProKa or Chimera 
	*Protonation of the protein structure is critical for docking (VDW and dipole moments)*
##### Homology modeling
- if there is no experimental structure available, model it using MODELLER, Rosetta, ICM or [I-TASSER](gaps_ideas.md#bender_2021#idea2)
- incorporation of the ligand during modeling can help prevent pocket from collapsing during docking
##### Docking Parameters
- calibrate scoring functions 
- important to monitor contributions of each energy term to the total score
- if one term dominates, the score is over optimized to that term 
- ex: if docking score of a polar solvent-exposed pocket is dominated by VDW, large molecules will score high due to nonspecific surface contacts with target protein
- extrema sets can be used to measure whether the model prioritizing the right molecules
##### Control Calculations 
- controls guard from obvious failures
- decoy molecules can be used to determine whether the docking model is predicting as expected
- it is more likely know true actives than true inactives
- use property matched decoys. unrelated topologies and presumed inactive
- DUDE-Z server generated decoys for ligands 
- performance is evaluated by ***receiver-operator characteristic curves*** (true positive rate as a function of false positive rate). ***Area under the curve (AUC**)* is a metric to monitor performance of a virtual screen by a single number 

![[dock_performance_measures.png]]
- the log transformation of false positive rate enhances effect of early enrichment for true positives
	- important: only compounds ranked within top 0.1% are closely evaluated 
- can also evaluate based on ligand poses using RMSD or qualitative comparison to experimental 
##### Large Scale Docking Screen
- large libraries of molecules can be virtually screened against a target protein 
- ZINC20 database 
##### Hit Picking
- top0.1% in a huge docking screen might still leave us with 1 million molecules to consider 
- we need to take out false positives too
- additional filters are needed to identify promising hits with stop scoring 300k to 1million molecules
- filters can include for both positive and negative features
- select the best scoring cluster from clustering compounds by 2D similarity 
- scaffold clustering using Bemis-Murcko 
- visual examination of docked poses is useful (5000 compounds)
![[dock_hits_criteria.png]]

##### Experiments to test docking hits
- binding or functional assays
- [colloidal aggregation](https://www.sciencedirect.com/science/article/abs/pii/S1748013217305765)
- prefer to dock and test molecules with LogP <= 3.5 bc aggregators tend to have high LogP values and limited solubility 
- aggregators sequester proteins with little selectivity, partially denaturing and inhibiting them 
- can filter out from ZINC20 (low LogP compounds)
- concentration response curves for all targets
- before initial hits are advanced for optimization, make-on-demand libraries need to confirm the identity of the hit compound
- limitations of virtual library enumeration, chemical synthesis and downstream purification can result in mismatches between in silico predictions and in vitro tested compound 
- *Characterize promising compounds before optimization*
	- the identity and purity of the compound should be determined at minimum
	- direct experiment to test a docking pose prediction: determine experimental protein structure with drug docked in pose 
	- key anchor points need to be correct in the positions compared to the experimentally docked ligand
##### Selecting analogs for hit to lead optimization
- after virtual screen and docking hits were confirmed by different experiments, scaffolds are blueprints for exploring structure-activity relationships and further lead optimization 
- make-on-demand libraries will initially be delivered as racemic or stereomeric mixtures 
- purified stereoisomers can be purchased or made
- Hit Optimization:
	- can generate medicinal chemistry-inspired analog series 
	- or cheminformatic tools can be employed to virtually search purchasable chemical space for related scaffolds 
	- Use **SmallWorld** search engine to search **Enamine** **REAL** space 
	- supplier of parent compound might be able to provide a collection of molecules resembling the hit scaffold


##### Docking campaign with DOCK3.7 and ZINC20
- **Matching spheres**: ligand atoms mapping onto predefined hot-spots 
- generated from coordinated of heavy atoms from input bound ligand structure
- coordinated based on negative image of binding site generated from **SphGen**
- ligand rigid fragment are mapped onto matching spheres using **bipartite** **graph** **algorithm** 
- confirmations in the binding pocket are sampled using precalculated conformer libraries (**flexbiase**)
- conformer library: build using molecules divided into rigid fragment and different conformations are generated
- ligand poses are evaluated using physics based scoring function E = Evdw (van der waal) + Ees (electrostatic) + Elig_desol(ligand desolvation)
- contributions of target protein pocket are mapped on **pre-generated scoring grids**
	- scoring grid done by **Solvmap** program
- ligand desolvation energies are computed as the sum of the atomic desolvation of each ligand atom
	- calculated using AMSOL during ligand building and in conformer library
	- electrostatic and ligand desolvation depend on dielectric boundary

- Protocol
	1-4 prepared starting structure
	5-10 generate scoring grids and matching spheres 
	11-33 collects a set of control ligands for model evaluation 
	34-58 Control ligands are docked retrospectively to determine the models ability to identify actives from a pool of inactives
	59-64 Optimization of sampling 
	65-77 scoring evaluation with the same controls 
	78-88 extrema control set to examine for charge preferences in the scoring grids and
	89-103 small-scale in stock screen to ensure a computationally expensive large-scale prospective screen
	104-108 hit picking 
	![[dock_protocol.png]]
# Summary-- relevance to our project
- Retrospective Control Calculations 
	- 'in-stock’ compound set is used as an experimental control to guard against obvious sources of failures 
	- the model parameters will be tweaked for each type of control covalent library 
	- each tweaked model can then be used to dock each type of experimentally determined ligand actives (from Martin) 
	- "type" == warhead type of the ligands (ex: unsub acrylamide)
	- decoys of active and inactive compounds can be constructed and docked instead of using in stock compound sets (decoys created using DUDE-Z server and known active/inactive compounds for the given target)
	- known activates (positive controls): found in scientific literature ChEMBL/ZINC/available in-house

- Prospective Docking screen
	- after tweaking the model: large libraries can be screened against target 
	- ZINC2.0 DB has readily available compounds for testing
		- includes 3D conformer libraries of commercially available compounds 
		- most blond to make-on-demand libraries like Enamine (like unsubstituted_acrylamides_frag, beta_sub_acrylate_esters, etc)
	- will give a list of molecules rank-ordered by docking score 
	- best molecules can be used to experimentally test 

- Hit Picking 
	- visually filtering molecules
	- molecules with strained conformations are discarded
	- this paper has a clean hit picking criteria 

- Experiments to test docking hits
	- binding or functional assays
	- dock and test molecules with LogP <= 3.5 
	- concentration response curves
	- determining an experimental protein structure in complex with docking hit 
	- before hit optimization, important for make-on-demand libraries (from prospective docking screen) to confirm identity of hit compound

- Selecting analogs for hit to lead optimization 
	- newly obtained scaffolds can be used to explore structure-activity relationships and lead optimization 
	- subtle changes to starting compound to test particular interactions 

# How does DOCK3.7 work?
- ligands are placed in target pocket by mapping ligand atoms onto predefined hot spots/matching spheres 
- matching spheres
	- generated from coordinated of heady atoms form an input bound ligand structure 
	- and/or coordinates based on negative image of the binding site generated from SphGen
	- ligand rigid frags (ex: rings) are mapped onto matching spheres using bipartite graph algorithm 
	- db2 files have pre-calculated 3D conformer libraries for ligand conformation/orientation sampling in the binding pocket 
	- ligand poses are evaluated using physics based scoring function 
	- contributions of target protein pocket are mapped onto pre-generated scoring grids 
		- ChemGrid converts the VDW surface of binding pocket into a scoring grid
		- Electrostatic potentials within binding pocket are estimated by solving the Poisson-Boltzmann eq using QNIFFT 
		- Solvmap generates context-dependent desolvation energy scoring grinds 
		- Atomic desolvation energies are calculated during ligand building using AMSOL 