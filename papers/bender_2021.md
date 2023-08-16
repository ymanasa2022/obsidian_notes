## A practical guide to large-scale docking 

### Abstract 
-structure-based docking screens of large compound libraries
-establishing controls to avoid under sampling of configs is important 
-paper shows procedure to evaluate docking parameter for melatonin receptor
-uses DOCK3.7 

### Introduction
-DNA-encoded libraries: collection of small molecules linked to DNA that contains unique information about the identity and structure of each molecule. The DNA tags, or "bar codes", record the synthetic history of each molecule
-DNA encoded libraries are limited to aqueous solutions thus limiting chemical rxns and chemical libraries 
-'make on demand' libraries: Enamine 
-structure based molecular docking: simulations of docking many ligands to a protein 
-large scale docking is unable to simulate enough interaction terms to achieve chemical accuracy
-they only help eliminate molecules that are definitely unable to bind a target, [prioritizing ones that have a change](gaps_ideas#bender_2021#idea1)

### Large library docking workflow

![[large_docking_workflow.png]]
##### Structure Prep
-high resolution ligand-bound structure outperform ligand-free structures 
	-tools like SphGen, SiteMAp and FTMao can be used to identify potential ligand binding sites 
-small enclosed binding pockets perform better than flat and solvent-exposed binding sites which are typical of ppi 
-mutations in high res structures should be reverted to wild type (missing side chains and loops should also be added)
-can include water molecules. treat them as non-displaceable parts of the protein structure. include them esp water molecules are enclosed in the targeted binding pocket 
-Buffer components should be removed
-Hydrogen atoms should be removed and remodeled. Hydrogens part of certain residues can be modeled using programs like Reduce (included in DOCK3.7), Maestro, ProKa or Chimera 
*Protonation of the protein structure is critical for docking (VDW and dipole moments)*
##### Homology modeling
-if there is no experimental structure available, model it using MODELLER, Rosetta, ICM or [I-TASSER](gaps_ideas#bender_2021#idea2)
-incorporation of the ligand during modeling can help prevent pocket from collapsing during docking

##### Docking Parameters
-calibrate scoring functions 
-important to monitor contributions of each energy term to the total score
-if one term dominates, the score is over optimized to that term 
-ex: if docking score of a polar solvent-exposed pocket is dominated by VDW, large molecules will score high due to nonspecific surface contacts with target protein
-extrema set can be used to measure whether the model prioritizing the right molecules
##### Control Calculations 
-controls guard from obvious failures
-decoy molecules can be used to determine whether the docking model is predicting as expected
-it is more likely know true actives than true inactives
-use property matched decoys. unrelated topologies and presumed inactive
-DUDE-Z server generated decoys for ligands 
-performance is evaluated by ***receiver-operator characteristic curves*** (true positive rate as a function of false positive rate). ***Area under the curve (AUC**)* is a metric to monitor performance of a virtual screen by a single number 

![[docking_performance_measures.png]]
-the log transformation of false positive rate enhances effect of early enrichment for true positives
	-important: only compounds ranked within top 0.1% are closely evaluated 
-can also evaluate based on ligand poses using RMSD or qualitative comparison to experimental 