# Step 1: adding Si to covalent bond point 
`/home/ymanasa/turbo/CovalentLibs/martin_cdd/martin_cdd_09132023`.smi
- created a `.smi` file with SMILES given by Martin on Sep 13, 2023 (also in CDD Vault)
- example `.smi`:  `/home/ymanasa/turbo/CovalentLibs/unsubstituted-acrylamides/fragments/smiles/unsub.frag.acrylamides.smi`
- script to run for `Si` replacement: `/home/ymanasa/turbo/CovalentLibs/scripts/
- created `martin_cdd_09132023.ism` in `/home/ymanasa/turbo/CovalentLibs/martin_cdd`
	- used columns C D to create tab spaced file `martin_cdd_09132023.smi` 
	- use one of the `heterocyclic-nitrile.py` files to convert the nitril groups in all the SMILES in `martin_cdd_09132023.smi`
	- look at line 19 SMIRKS reaction in smarts.plus 
![[heterocyclic-nitril.png]]

![[heterocyclic-nitril-1.png]]

![[heterocyclic-nitrile-2.png]]

![[heterocyclic-nitrile-3.png]]

- in conda environment `docking` , I installed openeye tools using: 
	`conda config --add channels openeye`
	`conda install openeye-toolkits`

- changed the python script from python 2 to python 3 
`/home/ymanasa/turbo/CovalentLibs/scripts/heterocyclic-nitrile-1-py3.py`

- Additionally, all the compounds that martin sent follow the SMIRKS pattern in heterocyclic-nitril-1.py
	- they have CN bonded to one aromatic C followed by aromatic N 
	- ![[martin_09132023_1aromaticC_1aromaticN.png]]
	- `[SiH3:1].[n:2][a:3][C:4]#[N:5]>>[n:2][a:3][C:4]([SiH3:1])=[N:5]`
	- used this in heterocyclic-nitrile-1-py3.py

- to add OE_LICENSE variable, run` setup_environment_new.sh` in `nfs/turbo/umms-maom/projects/TgCPL/docking-campaigns/docking_campaigns_local/`
![[ligand_prep_error_openeye.png]]
- run: `python heterocyclic-nitrile-1-py3.py ../martin_cdd/martin_cdd_09132023.ism` 
	- gives `output.ism` with Si 
# Step 2: creating db2 files
using [tldr](https://tldr.docking.org/) we can create the db2 files for all the ligands 
- the db2 files contain all the poses of each ligand 
- using the build3d38 module to make db2 files 
- the input is the output.ism file generated in the last step 

can check job status
![[job_status_tldr.png]]
- moved the resulting zip file to `/home/ymanasa/turbo/CovalentLibs/martin09132023_cdd`
- unpacking all tar in `/home/ymanasa/turbo/CovalentLibs/martin09132023_cd`
- created `database.sdi` in above of paths to all `.db2.gz`
- moved `database.sdi` to my databases 
`/nfs/turbo/umms-maom/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/martin09132023_cdd`

# Errors
- the db2 files from tldr seem to be incompatible with DOCK3.7 i am using for docking 
- Miguel suggests to use openbabel to convert my SMILES (output.ism-- has Si) into mol2 and then use tldr build3d_mol2 to get db2 gz files for input into DOCK3.7
- cloned the repo onto my computer 
	- followed instructions in INSTALL file of repo
	- tried running test cases and failed 1 test:
	![[openbabel_local_test_fail.png]]
- cloning on greatlakes at `/home/ymanasa/opt/`
- OpenBabel didnt work for me
	- asked Miguel to do it instead 

# Step 1a: mol2 from SMILES
## Oct 30, 2023
- using rdkit to create mol2 using SMILES 
	- Miguel wrote gen_sdf.py and made multi-molecule sdf file using my SMILES (after Si added)
	- the sdf file is then converted into mol2 file using rdkit or open babel
- this mol2 file can be input into tldr build3d_mol2 (`manasa_rdkit.mol2` was input file)

# Need to prep ligands using build_ligand_tldr.sh: refer to [[debugging_dock3.8]]
sh /home/ymanasa/turbo/opt/DOCK-debug/ucsfdock/ligand/generate/build_ligand_tldr.sh build3d38_results.zip --covalent