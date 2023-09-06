happening in: `/home/ymanasa/turbo/projects/TgCPL/docking/docking-campaigns/docking_campaigns_local/`
- use method to dock a library of commercially available ligand types assessed in previous step
- make library using guide to pharmacology.com, chemb, pubchem, binding db
- one zinc id might correspond to different chmbl molecules. toxoplasma cpl and human cpL

- Docking being performed on greatlakes in turbo: `/home/ymanasa/turbo/projects/TgCPL/docking/docking-campaigns/docking_campaigns_local`
	- it is connected to a github repo (docking_campaigns)

- *Have to run source setup_environment.sh every time you start a new session*
- start docking process by running `$DOCK_TEMPLATE/scripts/wizard.sh` in home docking dir
- Have to add pdb code to 1_make_structure.sh in `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/structures/tgcpl_20230901` to make receptor structure 
![[1_make_structure_edits.png]]

- To find out which covalent_residue_number to use in the `/home/ymanasa/turbo/projects/TgCPL/docking/docking-campaigns/docking_campaigns_local/prepared_structures/tgcpl_20230830/1_prepare_structure.sh `file:
	- Open the target ligand (Toxoplasma CPL ***3F75***) in pymol and open a reference protein that is similar enough to the target that has a ligand in the crystal structure (CPK ***301G***-- got this from the excel sheet called TgCPL activities).
	- Estimate where the ligand in 301G is in contact with residue in 3F75 to determine COVALENT_RESIDUE_NUMBER

![[pymol_ligand_contact_view.png]]

- Had to add line to detect with python because when the slurm script ran, the right python in the environment was not being used
![[1_prepare_structure_edits 1.png]]

- make sure INDOCK file in `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/prepared_structures/tgcpl_20230901/dockfiles` exists and looks ok
- ![[dockfiles_INDOCK_File.png]]
- also check `docking/trim.electrostatics.phi` file. it should look like: 
- ![[trim.electrostatics.phi_start.png]]
- middle of the same file: 
![[trim.electrostatics.phi_middle.png]]
- add these lines to `2_finalize_structure.sh` before running it: 
![[2_finalize_structure_edits.png]]

- go back to home docking dir (`/home/ymanasa/turbo/projects/TgCPL/docking/docking-campaigns/docking_campaigns_local`) and run `$DOCK_TEMPLATE/scripts/wizard.sh`


# Debugging 09/03-09/06
For some reason docking for neither a previous example or covalent docking to TgCPL is working after the docking_campaigns directory was moved from /home/ymanasa. 

Currently trying to rerun example (androgen) done with Marissa in /home/ymanasa
![[debug_androgen_ex_run.png]]
It is working just fine. Note the export path information. That is probably not the same when run from turbo/. Need to compare. This test ran successfully. 

- Ran two different tests with TgCPL in /home/ymanasa. tgcpl_20230901 (NOT covalent docking) and tgcpl_cov_20230905 (COVALENT docking). 
	- docking runs happening for: tgcpl_20230901,zinc_instock,tgcpl_test_new,20230905
	- preparing structures for tgcpl_cov_20230905
		- running docking tgcpl_cov_20230905,zinc_instock,tgcpl_cov_test,20230906
		- ignored the following errors while preparing structure: 
		![[covalent_docking_structure_prep_errors.png]]
		- export path info: ![[export_path_home_cov_tgcpl.png]]
- Things are at least running but memory issues didnt let the jobs finish.
- Path issues must be resolved if you want to run from turbo/
- 