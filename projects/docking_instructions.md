Docking examples done in `/home/ymanasa/TgCPL_docking`
## System Setup (on greatlakes)
1. `mkdir /home/<user>/opt/` in your home directory (/home/ymanasa/opt/)
2. `cd /home/<user>/opt/`
3. `git clone https://github.com/maomlab/dock_campaign_template.git`
4. `cd ${HOME} && ln -s /nfs/turbo/umms-maom turbo` to create a symlink to the original docking scripts. ***THESE SCRIPTS SHOULD NOT BE CHANGED.*** 
5.  `bash Miniconda3-py310_23.1.0-1-Linux-x86_64.sh` (get script from miniconda webpage)
6. use `/home/ymanasa/opt/dock_campaign_template/docking_env.txt` to create a conda env
	-  `conda create --name <env> --file <requirements.txt>`
	- `conda activate <env>` 
7.  `mkdir /home/<user>/<receptor>_docking` 
	directory where docking will be done and results saved (ex: /home /ymanasa/TgCPL_docking/)
8. `mkdir /scratch/scratch/maom_root/maom0/<user>/DOCK_common/`
## Database Creation 
will write this later
## Make Structure  
1. run `source setup_dock_environment.sh` in `/home/<user>/<receptor>_docking`
	- change these lines before running setup_dock_environment.sh:
		1. change lines 16-19 with appropriate SLURM info
		2. line 21 with correct scratch directory path
		3. line 22 where dock_campaign_template repo was cloned (ex:  `${HOME}/opt/dock_campaign_template`) 
		4. line 24 with right DOCK version and path (using 3.8 here-- `export DOCKBASE=${HOME}/turbo/opt/DOCK-dev/ucsfdock`)
		5. line 29 with path to ZINC databases (everyone should use:  `ZINC3D_PATH=" ${HOME}/turbo/ZINC_mirror/published/3D"`)
	***must `source setup_dock_environment.sh` every time you open a new shell***
2. run `$DOCK_TEMPLATE/scripts/wizard.sh` in `/home/<user>/<receptor>_docking` 
3. choose option `1 Make Structure`
4. choose `TEMPLATE_CUSTOM_PDB` 
5. type `<structure_name>`. The words won't appear while you type them. 
	a directory with the name and date will be made once you hit enter.
6. navigate to the newly created `<structure_name>/`directory within `structures/`
7. edit `1_make_structure.sh`
	1. fill line 11 if getting PDB structure from web 
		- if not getting PDB from the web,
			1. line 18: add `ln -s <pdb_name>.pdb raw.pdb`
			2. comment out lines 11, 16 and 17
	2. to fill lines 12-14:
		- open the receptor structure PDB in PyMOL
		- line 12: receptor chain the ligand is in (`A`)
		- line 13: chain the ligand is in (`A`)
		- line 14: three letter ligand code (`EST`) 
		- ![[dock_pymol_ex.png]]
8. run `source 1_make_structure.sh`
	- output: receptor atoms (rec.pdb) and ligand atoms (xtal-lig.pdb)
9. return to `/home/<user>/<receptor>_docking` 
## Prepare Structure
1. run `$DOCK_TEMPLATE/scripts/wizard.sh` in `/home/<user>/<receptor>_docking/` 
2. choose option `2 Prepare Structure`
3. choose structure made `<structure_name>/`
4. choose option `4 TEMPLATE_STANDARD`
	- makes a directory called `prepared_structures/` with `1_prepare_structure.sh`
5. `cd prepared_structures/`
6. `source 1_prepare_structure.sh`
7. `cd dockfile/`
8. `vi INDOCK`
	- edit lines 19-21 and 29: increase values to 100 to include ALL atoms in ligands for docking
## Docking Run
1.  run `$DOCK_TEMPLATE/scripts/wizard.sh` in `/home/<user>/<receptor>_docking/` 
2. choose option `4 Docking Run`
3. choose database 
4. choose prepared structure  `<structure_name>`
5. choose default docking name
	- creates `docking_runs/` with `1_submit.sh`
	- change line 17: `bash /home/ymanasa/<receptor>_docking/dock_submit.sh`
6. ` cp ${DOCK_TEMPLATE}/scripts/dock_submit.sh /home/<user>/receptor_docking/`
7. `vi /home/<user>/receptor_docking/dock_submit.sh`
	- line 32: add `export USE_DB2=true`
	- line 33: add `export USE_DB2_BATCH_SIZE=1`
	- line 34: add `export USE_DB2_TGZ=false`
	- line 38: change to `export DOCKEXEC=${DOCKBASE}/docking/DOCK/dock64`
8. `cd docking_runs/<receptor>_<date>_<db_name>/` 
9. `source 1_submit.sh`
10. check `results/<pose#>/test.mol2.gz.0` binary 
	- should be full and not with just one line


http://tebresearch.org/2014.10.30.a.DOCK_3.7_tutorial.pdf 