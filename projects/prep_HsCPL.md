All the assays we have from ChemBL (HsCPL_CHEMBL3837_ligand_activities) have target organism: CHEMBL3837
UniProt ID: P07711
PDB: 1CJL (Best resolution)
![[hscpl_chembl_assays.png]]

Matt put together a structure list for all cathepsins in various organisms (on drive, in [TgCPL Activities](https://docs.google.com/spreadsheets/d/1Lo0Nc6OFRyUe0arYsGTmi4eR1rFFTiq_GEcoAIC9rmE/edit#gid=1608986737). Upon filtering for Homo sapien cathepsins, there's a whole bunch of them 
- Searching for a structure with a propeptide/ligand bound to know where to dock to 
- 3HWN, CATHEPSIN L with AZ13010160. Kenny, P., Morley, A. has ligand 
![[3HWN_HsCPL_w_ligand.png]]

- 3OF9, Structural Basis for Irreversible Inhibition of Human Cathepsin L by a Diazomethylketone Inhibitor, Shenoy, R.T., Sivaraman, J.
![[3OF9_HsCPL_w_inhibitor.png]]
- 3OF8, Structural Basis for Reversible and Irreversible Inhibition of Human Cathepsin L by their Respective Dipeptidyl Glyoxal and Diazomethylketone Inhibitors, Shenoy, R.T., Sivaraman, J.
![[3OF8_HsCPL_w_inhibitor.png]]
- might be more relevant to look at nitrile inhibitors since Martin's first batch have nitrile warheads
- 5MAJ, CATHEPSIN L IN COMPLEX WITH 4-[cyclopentyl(imidazo[1,2-a]pyridin-2-ylmethyl)amino]-6-morpholino-1,3,5-triazine-2-carbonitrile, Kuglstatter, A., Stihle, M., Benz, J.
	- Bolded in the [TgCPL Activity](https://docs.google.com/spreadsheets/d/1Lo0Nc6OFRyUe0arYsGTmi4eR1rFFTiq_GEcoAIC9rmE/edit#gid=1608986737) sheet for some reason 
![[5MAJ_HsCPL_w_nitrile_bolded.png]]
The rest of the google sheet are other cathepsins
##### Ignore this one (noncovalent)
- 2YJ2, CATHEPSIN L WITH A NITRILE INHIBITOR, Banner, D.W., Benz, J.M., Haap
	![[2YJ2_HsCPL_w_nitrile_inhib.png]]
	- upon further reading into this paper for the above ligand: [CATHEPSIN L WITH A NITRILE INHIBITOR](https://chemistry-europe.onlinelibrary.wiley.com/doi/10.1002/cmdc.201100353), it seems like the paper is ***Halogen Bonding at the Active Sites of Human Cathepsin L and MEK1 Kinase: Efficient Interactions in Different Environments***  and talks above noncovalent interactions with the active site using ligands with halogens
	- check if the same residue is involved in the drug docking

# Target Prep 
- [[bender_2021]] suggests using high resolution structure for covalent docking
	- the best one we have of HsCPL is 1CJL ![[1cjl_pymol_messed_up.png]]
	- it doesnt have a ligand/propeptide bound to it. also looks like a mess
	- can find what the reactive residue is using the other structures
	- align and find same residue in PyMOL
- Comparing 5MAJ and 3OF8: 
`fetch 5MAJ, type=pdb1`
`fetch 3OF8, type=pdb1`
`align 5MAJ,  3OF8`
> `RMSD =    0.207 (1357 to 1357 atoms)`
(smaller the rmsd the better)
- RMSD between 3HWN and 3OF9
>  `RMSD =    0.340 (1347 to 1347 atoms)`
- Align all: 
	- click 'A' aka Action on each loaded pdb -> align to molecule -> 3HWN 
	- aligned all to 3HWN 
- Executive: RMSD =    0.281 (194 to 194 atoms)  
 Executive: object "aln_3OF9_to_3HWN" created.

 Executive: RMSD =    0.308 (198 to 198 atoms)  
 Executive: object "aln_3OF8_to_3HWN" created.

 Executive: RMSD =    0.291 (199 to 199 atoms)  
 Executive: object "aln_5MAJ_to_3HWN" created.