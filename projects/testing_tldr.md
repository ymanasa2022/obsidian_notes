# Rebuild Ketone Based Enones with Si
- rebuilding a subset of enamine ketone_based_enones using ***build3d_dock38***
	- the enamine libraries might have older formats of the db2 files that are not compatible with dock3.8
	- the input used was the file with smiles, zinc id and third column after Si atoms were added
	- the output gz file from tldr seems incomplete 
		- there's only a few db2 files and doesn't seem to be more than one molecule per db2 file  
	- database will be here: `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/partial_ketone_enones`
- also rebuilt same subset using mol2 file (from Miguel) ***build3d_mol2***
	- want to check whether output has same missing molecules or not
	- they dont have same missing outputs

# Testing Non-Covalent Dock3.8
## db2 made with build3d38
- test non-covalent docking with partial ketone covalent library dock3.8 
- `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/docking_runs/tgcpl_20231115,partial_ketone_enones_build3d38,20231115/`
- had to change `${DOCK_TEMPLATE}/scripts/dock_submit.sh` path to dock64
- had to rerun blastermaster and use a structure prepared for non-covalent docking 
- running into ***`tarfile.ReadError: bad checksum`***
# Testing Covalent Dock3.8
## db2 made with build3d38
- test covalent docking with partial ketone covalent library dock3.8 on tgcpl 
	- `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/docking_runs/tgcpl_cov_20230911,partial_ketone_enones_build3d38,20231114_prior_blastermaster_rerun
	- `source set_up_environment_DOCK38` before running 
- had to change `subdock.bash` script path a little 
- had to change INDOCK first line to *DOCK 3.8 parameters*
- had to change path to dock64 (take out bin/from path)
	- running into some errors 
	- ![[cov_dock38_partial_ketone_error.png]]
- Miguel suggest rerunning blastermaster (done rerunning)
- rerunning docking (`/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/docking_runs/tgcpl_cov_20230911,partial_ketone_enonesbuild3d38,,20231115`)


# Rebuilding Keton Based Enones without Si 2 col
- created a subset of ketone enones library with only SMILES and ZINC ID
	- prior to adding Si atoms 
	- `/Users/ymanasa/OneDrive - Michigan Medicine/1PhD/omeara_lab/TgCPL/Docking/partial_ketone-based-enones_test/partial_ketone_enones_no_Si.ism`
- rebuilding db2 files using this on build3d38 
- this worked to crate db2 files

# Rebuilding Keton Based Enones with Si 2 col
-  created a subset of ketone enones library with only SMILES and ZINC ID
	- after adding Si atoms
- this worked to create db2 files
- dock with tgcpl and dock3.8
- made database.sdi file using db2 files from: `/home/ymanasa/turbo/CovalentLibs/partial_ketone_enone_dock38test/build3d38_redo/H00M500`
## Docking to tgcpl covalently 
- `tgcpl_cov_20230911,partial_ketone_enones,new_database,20231116/`
- ![[bad_zip_new_db2_cov.png]]
# Testing DOCK3.8 using tldr output from Miguel
- database.sdi created in `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/miguel_working_test/mol2_build3d38`
- non-covalent docking with dock3.8 on tgcpl (noncov prepped structure)
- ![[tar_read_error_dock38_miguel.png]]
## Docking using Miguel's prepped structure (ADA) and the a tldr produced database 
- known to work with Miguel's setup 
- made a subset of the database he provided (in database.sdi)