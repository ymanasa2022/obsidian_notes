# Oct 26, 2023
docking martin09132023 after [[lig_prep_martin09132023]]

`/nfs/turbo/umms-maom/projects/TgCPL/docking-campaigns/docking_campaigns_local/docking_runs/tgcpl_cov_20230911,martin09132023_cdd,,20231026`

docking right now 
Error: ligand db2 gz files might not be good
![[martin_ligands_failed.png]]
![[martin_tgcpl_db2gz.png]]

Take a look at one of the db2.gz files that did work for docking: ![[aldehyde_based_gz.png]]
They seem the same... not sure whats up 

# Feb 8, 2024 
- revisiting since covalently prepped ligands and tar issue should be solved 
- refer to [[debugging_dock3.8]] for how to fix the above issue
## Structure
- selected PDB 3F75
- `structure/tgcpl_3F75_20231204/`
- receptor chain A 
- ligand chain A
- ligand coords come from aligned human cathapsin structure to tgcpl (lig 7KH)
## Prepped Structure 
- `prepared_structures/tgcpl_cov_3F75_20231204/`
- standard blastermaster to protonate receptor 
- protonated receptor through covalent blastermaster 
- change INDOCK appropriately (yes for covalent docking)
## Docking Run
- need to change $DOCKEXEC and $DOCKBASE paths in 1_submit.sh 
	- remove bin before dock64
	- remove slurm after submit
- errors; refer to [[debugging_dock3.8]]

# Feb 9, 2024 
## Docking Run
- docking to tgcpl with martin's ligands in: `tgcpl_cov_3F75_20231204,martin09132023_cdd,,20240208/`
- database.sdi file has all the db2.tgz ligand files 
- you need to use DOCK38 scripts instead of DOCK-debug scripts for docking
- not working :( 
	- some seemed to have worked! 
		- eg. 121, 4
- tested with JRH-10-3P.0.N.db2.tgz which doesn't have D block
	- seems to work (`results_JRH-10-3P.0.N_noD/`)
- testing with another no D block molecule (`263022.0.N.db2.tgz`)
	- doesnt work (`results_263022.0.N_noD/`)
	- `ligand did not contain covalent atom`
- testing with the D block of `263022.0.N` -> `263022.0.N.D.db2.tgz`
	- doesnt work (`results_263022.0.N.D`)
`The first line in D section is brokenD     42  7   +2.5667   -1.3802   -0.5976`

## Sanity Check: Running Tldr again on Si subbed martin ligands
- smiles file:` /home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/martin09132023_cdd/smiles/martin_cov_09132023.ism`
- tldr running buid3d38
- dont think this is the issue


## Next Steps 2/13/24 discussion
Martin ligands: actives 
Decoy for Martin ligands: small world can generate acetyl-nitrile compounds (ones that can be converted using the SMARTS pattern) 
Higher log p are more hydrophobic-> in tranches of zinc 
Enumerated sets from Martin 
Covalent libraries 
Targets: tgcpl and hscpl (diff crystal structures for hscpl) and mouse one 
What is the best set up for each structure? How do we prioritize ligands from it— aggregate assessment of the ligands? 
Come up with dock scores to ligands