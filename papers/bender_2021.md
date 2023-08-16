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

### Structure Prep
-high resolution ligand-bound structure outperform ligand-free structures 
	-tools like SphGen, SiteMAp and FTMao can be used to identify potential ligand binding sites 
-small enclosed binding pockets perform better than flat and solvent-exposed binding sites which are typical of ppi 

