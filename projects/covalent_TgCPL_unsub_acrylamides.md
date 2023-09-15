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
		- try running all these scripts sequentially: source 1_prepare_structure.sh; source 2_prepare_structure.sh; source 3_prepare_structure.sh; source 4_prepare_structure.sh; source 2_finalize
		- this didnt work
		- keeping all files separate, run one after the other manually 1-4 prepare_structure.sh scripts 
# Docking run: 
- docking upon `/prepared_structures/tgcpl_cov_20230911`
- `tgcpl_cov_20230911,unsubstituted_acrylamides_frag,,20230914`
- using unsub acrylamides DB 
### Error: ![[segmentation_fault_tgcpl_unsub_acrlyamides.png]]