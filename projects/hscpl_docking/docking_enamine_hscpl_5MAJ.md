# Step 1: Making the structure 
using `source setup_dock_environment_DOCK38.sh`for prep structure step
on greatlakes, in `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local`
- wizard -> 1) TEMPLATE_CUSTOM_PDB
- `structures/hscpl_5MAJ_20231023/`
- ![[hscpl_5maj_ligand_resid.png]]
- ![[hscpl_5maj_make_structure.png]]
	- output: separate files for receptor (rec.pdb) and ligand (xtalg-lig.pdb)
	- DOCK is using ligand 7KH for more accurate sampling 
# Step 2: Preparing the structure 
wizard -> 3) Prepare Structure 
COVALENT_RESIDUE_NUMBER = 25 
- 1_prepare_structure: 
	- ![[prep_structure_hscpl_5maj.png]]
- 2_prepare_structure:
	- getting this error:
		- ![[prep_structure_hscpl_5maj_error.png]]
		- comparing tgcpl 2_prepare_structure.sh -> blastermaster.sbatch file and it looks like DOCK3.8 was used for structure prep but DOCK3.7 is later used for docking runs
		![[blastermaster_slurm_diff_tgcpl_hscpl.png]]
		- using DOCK3.8 for prep structure step by changing $DOCKBASE in setup_dock_environment_new.sh
			- `export DOCKBASE=${HOME}/turbo/opt/DOCK-dev/ucsfdock`
			- instead of: `export DOCKBASE=${HOME}/turbo/opt/DOCK37`
# Step 3: Docking Run
wizard -> 4) Docking Run
- change back $DOCKBASE to DOCK3.7 in setup_dock_environment_new.sh 
## aldehyde_based_cyanoacrylamides
- `hscpl_5MAJ_20231023,aldehyde_based_cyanoacrylamides_frag,,20231025/`

i think slurm job needs more time

- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## alkyl_halides
- `hscpl_5MAJ_20231023,alkyl_halides_frag,,20231025/`
i think slurm job needs more time
- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## alpha_sub_acrylate_esters
- `hscpl_5MAJ_20231023,alpha_sub_acrylate_esters_frag,,20231025/`
- docking right now
- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## beta_sub_acrylate_esters
- `hscpl_5MAJ_20231023,beta_sub_acrylate_esters_frag,,20231025/`
- docking right now
- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## heterocyclic_nitriles
- `hscpl_5MAJ_20231023,heterocyclic_nitriles_frag,,20231025/`
- docking right now
- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## ketone_based_enones_frag
- `hscpl_5MAJ_20231023,ketone_based_enones_frag,,20231026`
- docking right now
- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)

## unsubstitute_acrylamides_frag
- `hscpl_5MAJ_20231023,unsubstituted_acrylamides_frag,,20231026`
- docking right now
- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)