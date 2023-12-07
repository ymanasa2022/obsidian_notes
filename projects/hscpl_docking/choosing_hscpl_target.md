# Choosing a HsCPL structure
All the assays we have from ChemBL (HsCPL_CHEMBL3837_ligand_activities) have target organism: CHEMBL3837
UniProt ID: P07711
PDB: 1CJL 
![[hscpl_chembl_assays.png]]

Matt put together a structure list for all cathepsins in various organisms (on drive, in [TgCPL Activities](https://docs.google.com/spreadsheets/d/1Lo0Nc6OFRyUe0arYsGTmi4eR1rFFTiq_GEcoAIC9rmE/edit#gid=1608986737). Upon filtering for Homo sapien cathepsins, there's a whole bunch of them 
- Searching for a structure with a propeptide/ligand bound to know where to dock to 
- 3HWN, CATHEPSIN L with AZ13010160. Kenny, P., Morley, A. has ligand 
![[3HWN_HsCPL_w_ligand.png]]

- 3OF9, Structural Basis for Irreversible Inhibition of Human Cathepsin L by a Diazomethylketone Inhibitor, Shenoy, R.T., Sivaraman, J.
![[3OF9_HsCPL_w_inhibitor.png]]
- 3OF8, Structural Basis for Reversible and Irreversible Inhibition of Human Cathepsin L by their Respective Dipeptidyl Glyoxal and Diazomethylketone Inhibitors, Shenoy, R.T., Sivaraman, J.
![[3OF8_HsCPL_w_inhibitor.png]]

### might be more relevant to look at CPLs with nitrile inhibitors since Martin's first batch have nitrile warheads
- 5MAJ, CATHEPSIN L IN COMPLEX WITH 4-[cyclopentyl(imidazo[1,2-a]pyridin-2-ylmethyl)amino]-6-morpholino-1,3,5-triazine-2-carbonitrile, Kuglstatter, A., Stihle, M., Benz, J.
	- Bolded in the [TgCPL Activity](https://docs.google.com/spreadsheets/d/1Lo0Nc6OFRyUe0arYsGTmi4eR1rFFTiq_GEcoAIC9rmE/edit#gid=1608986737) sheet for some reason 
![[5MAJ_HsCPL_w_nitrile_bolded.png]]
The rest of the google sheet are other cathepsins
##### Ignore this one (noncovalent)
- 2YJ2, CATHEPSIN L WITH A NITRILE INHIBITOR, Banner, D.W., Benz, J.M., Haap
	![[2YJ2_HsCPL_w_nitrile_inhib.png]]
	- upon further reading into this paper for the above ligand: [CATHEPSIN L WITH A NITRILE INHIBITOR](https://chemistry-europe.onlinelibrary.wiley.com/doi/10.1002/cmdc.201100353), it seems like the paper is ***Halogen Bonding at the Active Sites of Human Cathepsin L and MEK1 Kinase: Efficient Interactions in Different Environments***  and talks above noncovalent interactions with the active site using ligands with halogens
	- check if the same residue is involved in the drug docking

- [[bender_2021]] suggests using high resolution structure for covalent docking
	-  one we have of HsCPL is 1CJL ![[1cjl_pymol_messed_up.png]]
	- it doesnt have a ligand/propeptide bound to it. also looks like a mess
	- can find what the reactive residue is using the other structures
	- align and find same residue in PyMOL

(smaller the rmsd the better)
- Align all: 
	- click 'A' aka Action on each loaded pdb -> align to molecule -> 3HWN 
	- aligned all to 3HWN 
		- 3OF9 RMSD =    0.281 (194 to 194 atoms)  
		- 3OF8 RMSD =    0.308 (198 to 198 atoms)
		- 5MAJ RMSD =    0.291 (199 to 199 atoms)  
 
- for now find which residue binds to the ligand and use the highest quality structure for docking
list all-- lower the resolution the better:
5MAJ (1.00 Å)
3OF8 (2.20 Å)
3OF9 (1.76 Å)
3HWN (2.33 Å)
1CJL (looks like a mess in some settings in pymol) ( 2.20 Å)

Final: 5MAJ (1.00 Å)
- select residues using shift click (do after setting `selecting` to `residues`)
- residue 25 CYS in 5MAJ creates a covalent bond to the ligand 
- ![[covalent_bond_hscpl_5MAJ.png]]
- in 3OF8: residue 26 CYS creates covalent bond 
- in 3OF9: residue 26 CYS creates covalent bond
- in 3HWN: residue 25 CYS creates covalent bond 
going to use 5MAJ for now since it has highest resolution 
