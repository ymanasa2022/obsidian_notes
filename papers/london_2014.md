## *Covalent Docking of Large Libraries for the Discovery of Chemical Probes*

### Abstract
- chemical probes that form covalent bonds with protein target show higher selectivity, higher potency and utility 
- but, protein0reactive compounds are avoiding in docking campaigns 
- method to screen electrophilic small molecule libraries 
- target: protein nucleophiles 
- web server: covalent.docking.org aims to help us find small molecules to test for activity against my biological target for which I have a structure

### Introduction 
- enhancing properties: covalent bond formation with nucleophilic residues in target and that are absent from off-targets
- warheads: reactive functional groups 
- [unsolved problem](gaps_ideas.md#london_2014#gap1): how to identify a protein-binding scaffold that orients the electrophile while minimizing number of compounds that much be synthesized and tested 
- [issue](gaps_ideas.md#london_2014#idea1): combining classical non-covalent scoring with covalent restrains and bond energies
- issue2: developing compound libraries suited to covalent modification of proteins 
- authors show how to adapt the non-covalent docking program DOCK3.6 to large-scale, covalent virtual screening of electrophilic small molecules 
	- nine libraries of ligands bearing diff electrophilic small molecules 
- DOCKovalent to screen compound libraries against three targets 

### Methods
![[Covalent_docking_method.png]]

### Results
#### Retrospective Assessment
- authors used 23 bronic acid complexes/ligands to asses docking method. 
- accurately recovered == less than 2Å RMSD (docking structure compared to x-ray structure of ligand plus protein target)
- sometimes you might need to redetermine crystal structure of protein-ligand complex if docking results show different pose of a simple/obvious compound. if results good, covalently dock a library of <23k commercially available bronic acids to protein
- among top 4.5% of the library, they experimentally tested bronic acids with scaffolds that had not been previously docked 
- ligands were purchased and tested (5)
- lower ranked compounds were also purchased and tested instead of high ranking commercially unavailable compounds (6)
- inhibitory compounds: has Ki from 40nM to 3.55 uM, submicromolar potency(ligand efficiency LE 0.38-0.66)
- resemblance to known inhibitors: Tanimoto coefficients < 0.3 to existing broinic acids in ChEMBL
- **IC 50: the concentration of a particular drug that is needed to inhibit a given biological process to half of the maximum**
### Ligand Generation 
- ligand flexibility is sampled by generating ligand conformations prior to docking
- uses SMILES string of a ligand with a specific electrophile 
- OEChem library is used to convert the ligand to its final reacted form 
- the receptors nucleophilic atom involved in covalent bond is represented by a dummy atom 
- the ligands 3D structures and stereoisomers are built by Corina 
- then they are tautomerized and protonated by EPIK
- partial atomic charges and solvation energies are calculated for each structure using AMSOL 
- Omega generates conformations of the rigid starting electrophile
- collection of pre-generated ligand conformations in reacted stated is saved in DOCK readable flexibase format file

>>>>>>> 6a4c9439d45ce706481bee3e239554dbba6e7cb6
