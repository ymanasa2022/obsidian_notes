# Attempt 1
happening in: `/home/ymanasa/turbo/projects/TgCPL/docking/docking-campaigns/docking_campaigns_local/`
- use method to dock a library of commercially available ligand types assessed in previous step
- make library using guide to pharmacology.com, chemb, pubchem, binding db
- one zinc id might correspond to different chmbl molecules. toxoplasma cpl and human cpL

- Docking being performed on greatlakes in turbo: `/home/ymanasa/turbo/projects/TgCPL/docking/docking-campaigns/docking_campaigns_local`
	- it is connected to a github repo (docking_campaigns)

- *Have to run source setup_environment.sh every time you start a new session*
- start docking process by running `$DOCK_TEMPLATE/scripts/wizard.sh` in home docking dir
- Have to add pdb code to 1_make_structure.sh in `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/structures/tgcpl_20230901` to make receptor structure 
- not adding `LIGAND_CHAIN` and `LIGAND_RESID` because this pdb does not have a ligand bound
- 3F75 however, does have information about where a ligand might be bound (indicated by HETATM labels in pdb and in xtal-lig.pdb output)

***!! the ligand info is used for sampling but since we dont have a reference ligand for TgCPL, sampling might be slightly inaccurate !!***
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
		![[cov_docking_prep_errors.png]]
		- export path info: ![[export_path_home_cov_tgcpl.png]]
- Things are at least running but memory issues didnt let the jobs finish.
- Path issues must be resolved if you want to run from turbo/
# Docking to TgCPL: unsubstituted-acrylamides DB 
- using database: `/home/ymanasa/turbo/CovalentLibs/unsubstituted-acrylamides/fragments/`
- made .sdi file of unsubstituted-acrylamides in: `/home/ymanasa/turbo/CovalentLibs/unsubstituted-acrylamides/fragments/gz_files/unsub-acrylamide-frag.sdi`
- moved to `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/unsubstituted_acrylamides_frag` and called `database.sdi`
- structure in `structures/tgcpl_20230908/`
- preparing structure in `/prepared_structures/tgcpl_20230908`
	- docking files should be in `docking_campaigns_local/prepared_structures/tgcpl_20230908/docking`
- `docking_runs/ tgcpl_20230908,unsubstituted_acrylamides,,20230908/` 
	- *this did not work*
- testing tgcpl with zinc_instock database here: `tgcpl_20230908,zinc_instock,,20230908`
	- *this didnt work either*
#### Test: if covalent docking is working with androgen 
- testing androgen with zinc_instock database and previous example ligand androgen: `androgen_20230818,zinc_instock,,20230908` in turbo
		- *this worked*
- testing with zinc_instock and previous androgen but with COVALENT docking: `androgen_cov_20230908,zinc_instock,,20230908` in turbo 
		- *this worked*
- Issue: seems to be the prepared structure of tgcpl since androgen covalent docking works with zinc instock. could also be an issue with the database 
		- `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/prepared_structures/tgcpl_20230908/working/blastermaster.err` vs `../../androgen_cov_20230908/working/blastermaster.err` don't look the same
##### Verdict: ***Forgot to change the residue number in 1_prepare_structure.sh for tgcpl covalent docking***
# Re-docking to TgCPL with unsubstituted-acrylamides DB 
- using database: `home/ymanasa/turbo/CovalentLibs/unsubstituted-acrylamides`
- running in conda env `docking`
- structure (`tgcpl_cov_20230911`): using pdb *3F75* in 1_make_structure.sh
- prepare structure (`tgcpl_cov_20230911`): change `COVALENT_RESIDUE_NUMBER=422` to 31
	- ignoring sed errors![[cov_docking_prep_errors.png]]
	- works according to working/blastermaster.err and working/blastermaster.out files 
- docking run (`tgcpl_cov_20230911,unsubstituted_acrylamides,,20230911`): changed path to `dock_submit.sh` in `1_submit.sh`
	- ***did not work***
# Test: docking to TgCPL with zinc instock DB + covalent docking
- starting from docking_run (`tgcpl_cov_20230911,zinc_instock,tgcpl_zinc,20230911`): 
	- using `dock_submit.sh` from `docking_campains_local/`
		- ***did not work***
	- the OUTDOCK file for tgcpl (doesnt work) and androgen (works) shows that maybe the structure prep step did not go well since grid sizes changed significantly. that's the only difference I see. ![[dock_tgcpl_androgen_ZINC_OUTDOCK_diff.png]]
- in `/prepared_structures/tgcpl_cov_20230911/dockfiles/INDOCK`  delphi_nsize is 99 which might be wrong?
#### Test: androgen docking with unsub acrylamides DB 
- starting from docking_run step 
 (`androgen_cov_20230908,unsubstituted_acrylamides,,20230911`): 
	- using `dock_submit.sh` from `docking_campains_local/
	- ***did not work***
##### Verdict: *might be something wrong with the unsub acrylamides database* 
- fragments were used to make database.sdi instead of lead-like compounds 
#### Test: use lead-like compounds from unsub acrylamides to dock to TgCPL
- starting from docking_run step (`tgcpl_cov_20230911,unsubstituted_acrylamides_lead-like,,20230911`)
	- using `/unsubstituted_acrylamides_lead-like` DB instead of `/unsubstituted_acrylamides_frag`
	- ***did not work***
##### Conclusion: there might be something wrong with unsub acrylamides DB but also there is something wrong with TgCPL structure prep 

# Issue: 
- this line in 1_prepare_structure.sh is not working (removed from `1_prepare_structure.sh`) : 
`source ${DOCK_TEMPLATE}/scripts/dock_indock_tight_covalent.sh`
-  probably because the program doesnt wait for output from `dock_blastermaster_covalent.sh` run before running this last file. 
	- I moved all lines in `dock_indock_tight_covalent.sh` to `2_finalize_structure.sh` 
	- updated TEMPLATE_COVALENT file that makes `2_finalize_structure.sh` every time wizard is run (on Matt's github)
	- still need to update COVALENT_RESIDUE_NUMBER
## Resolved: 
- ![[cov_docking_prep_errors.png]]
- this error doesn't show but the WARNING messages are still there even after changes residue number to 31 including a couple other errors: ![[prepare_structure_warnings.png]]
- making new script 2_prepare_structure.sh with these lines: 
`source ${DOCK_TEMPLATE}/scripts/dock_blastermaster_covalent.sh \`
     `${COVALENT_RESIDUE_NUMBER} \`
       `${COVALENT_RESIDUE_NAME} \`
    ` ${COVALENT_RESIDUE_ATOMS}`
  - also to run lines after running `dock_blastermaster_standard.sh` in `1_prepare_structure.sh`, I made everything one single line using &&: `source ${DOCK_TEMPLATE}/scripts/dock_blastermaster_standard.sh && mv working working_standard && cp working_standard/rec.crg.pdb rec.pdb && mkdir working`
	- actually ended up diving all commands into 4 different shell scripts 
		- try running all these scripts sequentially: source 1_prepare_structure.sh; 2_prepare_structure.sh; 3_prepare_structure.sh; 4_prepare_structure.sh; 2_finalize
	
# Docking run: 
- docking upon `/prepared_structures/tgcpl_cov_20230911`
- `tgcpl_cov_20230911,unsubstituted_acrylamides_frag,,20230914`
- using unsub acrylamides fragments DB 
### Error: ![[segmentation_fault_tgcpl_unsub_acrlyamides.png]]


# Sep 18: Re-docking 
- docking upon `/prepared_structures/tgcpl_cov_20230911` using unsubstituted_acrylamides_frag
- `tgcpl_cov_20230911,unsubstituted_acrylamides_frag,,20230918`
- still doesnt work. talk to matt
	- matt tried with dock3.7, should work
- changed the `$DOCKTEMPLATE` path to DOCK 37 in `setup_environment.sh `
- got this error: ![[dock37_test.png]]
# Sep 20: Debugging Dock--Resolved
- the subdock.bash file comes from the `$DOCKTEMPLATE/docking/submit/slurm` directory but the path in `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/dock_submit.sh` is incorrect 
	- changed this; `bash ${DOCKBASE}/docking/submit/subdock.bash` to:
		- `bash ${DOCKBASE}/docking/submit/slurm/subdock.bash`
		- using dock_submit.sh from: `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/dock_submit.sh`
- ![[fewer_errors_dock37.png]]

- dock64 is not in DOCK37??? ![[no_dock64_in_DOCK37.png]]
	- might need to check dock_submit.sh file that matt was using
		- a dock_submit.sh script was not used in the prev testing sesh with matt. 1_run.sh == 1_submit.sh+dock_submit.sh in:  `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/docking_runs/tgcpl_cov_20230911,unsubstituted_acrylamides_frag,,20230923/1_run.sh` 
		- 1_run.sh uses the right path to dock64: `${DOCKBASE}/docking/DOCK/bin/dock64`
		- dock_submit.sh uses `${DOCKBASE}/docking/DOCK/dock64` - changing it to include` bin/`
- ![[scratch_dir_error_DOCK37.png]]
- try to running from `/nfs/turbo/umms-maom/nSMase2/fragment_screen/docking_runs/manasa_test1`
	- editing the setup_environment.sh file in `/nfs/turbo/umms-maom/nSMase2/fragment_screen`
		- leaving this to access matt's dock_campaign_template 
			- `export DOCK_TEMPLATE=/home/maom/opt/dock_campaign_template` instead of `/home/ymanasa/opt/dock_campaign_template`
		- that didnt work. permission issues: 
			- changed DOCK_TEMPALTE to `/home/ymanasa/opt/dock_campaign_template`
			- ![[DOCK_analysis_dir_DNE.png|1500]]

## Conclusions
Testing in: `/nfs/turbo/umms-maom/nSMase2/fragment_screen/docking_runs/manasa_test1`
- the only difference between Matt's environment and mine is that I use my DOCK_TEMPALTE : `/home/ymanasa/opt/dock_campaign_template` but matt uses: `/home/maom/opt/dock_campaign_template `
- path to python files is messed up ?
	- `/home/ymanasa/opt/DOCK/analysis/extract_all_blazing_fast.py`: [Errno 2] No such file or directory
	- `/home/ymanasa/opt/dock_campaign_template/analysis/` should be the correct path but analysis/ is empty
- This issue is only for analysis. Docking worked technically (make sure to set right DOCK version in `../docking_runs/tgcpl/INDOCK` file)
- realized that `extract_all_blazing_fast.py` is actually in `$DOCKBASE = /home/ymanasa/turbo/opt/DOCK37/analysis` NOT in `$DOCK_TEMPLATE=/home/ymanasa/opt/dock_campaign_template`
## Results analysis
- changes made to print statements in `$DOCKBASE/analysis/extract_all_blazing_fast.py` 
- cd to `/home/ymanasa/turbo/nSMase2/fragment_screen/docking_runs/tgcpl_cov_20230911,unsubstituted_acrylamides_frag,,20230928`
	- run: `ls -d results/* > dirlist` to make a list of results/# directories
	- cleanup: remove anything other than numbered directories 
	- run: `python $DOCKBASE/analysis/extract_all_blazing_fast.py dirlist extract_all.txt 100`
	- check:` extract_all.sort.uniq.txt` for unique docked poses sorted by total energies (lowest to highest, lowest is best)
	- run: `python $DOCKBASE/analysis/getposes_blazing_faster_py3.py '' extract_all.sort.uniq.txt 1000000 poses.mol2 test.mol2.gz.0 > poses_out.txt`
	- chimera: load poses.mol2 file into chimera 
#### Errors: 
- ValueError: could not convert string to float: '-'
- only happening for certain results/# directories
	- changing the dirlist file incrementally to figure out which run was the issue
		- `results/7/OUTDOCK.0` and `results/8/OUTDOCK.0` were causing this issue
			- Upon only keeping `results/7` in dirlist, ![[results_7_outdock_results_analysis_error.png]]
		- happening because the energies in `/results/7/OUTDOCK.0` has '-' and no number 
		- removing last line for `7/`:  `18 NC000037833832.0 1                       1  430664467    0.00  13        78         1      3     1     0.29    0.00   -4.85   4.12   -1.46    0.00    0.00    0.00    0.00     -`
		- removing last line for `8/`: `18 NC000155952023.0 1                       1  649980281    0.00  17       186         1      3     1     0.08    0.00   -7.13   5.00   -1.13    0.00    0.00    0.00    0.00     -`
		- worked for all after that 
#### Docking_Run Summary: 
- .db2.gz files like unsub-acrylamide-frag.1.db2.gz have multiple ligands for docking 
- it is unzipped in the scratch directory
- 10 poses for each ligand in the .db2.gz file are docked to the receptor
- the total energies can be found in the /docking_runs/receptor_name_DBtype/results/1/OUTDOCK.0 file 
- the OUTDOCK.0 file shows the ligands docked along with all the poses of each and the energies
- each db2.gz file has different number of ligands but 10 poses each unless the energies are too high (above the 100 limit set in INDOCK)
# Oct 6, 2023
## Premature job termination
might be the cause of the errors seen when analyzing the OUTDOCK.0 file
- ValueError: could not convert string to float: '-'
- add higher wall time and memory requests to the 1_submit.sh or1_run.sh docking script 
	- requesting 1GB mem per cp = 1000/768 = 1.3 cores (round down: 1 core)
	- requesting 6 hours wall time
- running test at: `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/docking_runs/tgcpl_cov_20230911,unsubstituted_acrylamides_frag,,20231006`
## Git hub repo update
Can't resolve unstagging deleted big files in order to avoid memory limit error during push
## Migration to /projects/TgCPL on turbo
moved tested `TgCPL + unsub_acrylamides` from `/nSMase2/fragment_screen/` to `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/`
- moved necessary scripts too 
- `setup_environment_new.sh` is the latest environment set up script and should be used before running DOCK 
- running with DOCK3.7 not 3.8 
## Changing scripts to reflect how things should be run
need to change scripts in `${DOCK_TEMPLATE}=/home/ymanasa/opt/dock_campaign_template` to reflect changes in how the scripts are written and set up  
- changed  
	- `/home/ymanasa/opt/dock_campaign_template/docking_runs/TEMPLATE_COVALENT/1_submit.sh` 
	- scripts for preparing the structure (1-4prepare_structure.sh and 5_finalize_structure.sh)
	- `/home/ymanasa/opt/dock_campaign_template/docking_runs/TEMPLATE_COVALENT/2_gather.sh `
		- divided into two files 1 and 2 

# Oct 9, 2023
## Premature job termination
- issue still seems to be wall time. job did not finish due to insufficient wall time request 
(can be seen in "Job 61963082 (rundock) Ended" email; Used CPU time:  05:55:39 and Res. Walltime : 06:00:00) 
- just going to rerun but with way bigger run time (48 hours) and increased req mem to 2GB 
- add higher wall time and memory requests to `setup_dock_environment_new.sh`
## Submitting pull request for changed scripts to reflect how things should be run
- since previous pull request was not resolved and closed, any new commits made on prepare_structure_fix branch is automatically added to previous pull request
- the pull request can be updated manually on github