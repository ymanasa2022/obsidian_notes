# Oct 10, 2023
## ENAMINE libraries
`/home/ymanasa/turbo/CovalentLibs/`
docking/docked the following:
- [x] alpha-sub-acrylate-esters
- [x] ketone-based-enones
- [x] unsub_acrylamides
- [x] beta_sub_acrylate_esters_frags
- [x] aldehyde-based-cyanoacrylamides
- [x] heterocyclic-nitriles
- [x] alkyl-halides
- [ ] di-amine-linkers
- [ ] fluorosulphones
- [ ] amines
- [ ] cyanamides
- [ ] vinyl-sulfone
- [ ] fmk
## unsub_acrylamides run
ran successfully, took around 12 hours and less than 1GB of memory 
- [x] docking finished
- [x] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
### pose generation
- run: `ls -d results/* > dirlist` to make a list of results/# directories
	- cleanup: remove anything other than numbered directories 
	- run: `python $DOCKBASE/analysis/extract_all_blazing_fast.py dirlist extract_all.txt 100`
	- check:` extract_all.sort.uniq.txt` for unique docked poses sorted by total energies (lowest to highest, lowest is best)
	- run: `python $DOCKBASE/analysis/getposes_blazing_faster_py3.py '' extract_all.sort.uniq.txt 1000000 poses.mol2 test.mol2.gz.0 > poses_out.txt`
	- chimera: load poses.mol2 file into chimera 
	
can be found here: `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/docking_runs/tgcpl_cov_20230911,unsubstituted_acrylamides_frag,,20231006`

![[tgcpl_unsub_acryl_N_angle_weird.png]]
## beta_sub_acrylate_esters_frags
- [x] docking finished
- [x] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## alpha-sub-acrylate-esters
`/home/ymanasa/turbo/CovalentLibs/alpha-sub-acrylate-esters/fragments/gz_files`
- ls -d /nfs/turbo/umms-maom/CovalentLibs/alpha-sub-acrylate-esters/fragments/gz_files/*.db2.gz > database.sdi 
- moved to `/nfs/turbo/umms-maom/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/alpha_sub_acrylate_esters_frag`
- [x] docking finished
- [x] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## ketone-based-enones
`/nfs/turbo/umms-maom/CovalentLibs/ketone-based-enones/fragments/gz_files`
- ls -d /nfs/turbo/umms-maom/CovalentLibs/ketone-based-enones/fragments/gz_files/*.db2.gz > database.sdi 
- moved to `/nfs/turbo/umms-maom/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/ketone_based_enones_frag`
- [x] docking finished
- [x] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## heterocyclic-nitriles
`/nfs/turbo/umms-maom/CovalentLibs/heterocyclic-nitriles/fragments/gz_files/`
- moved `database.sdi` to `/nfs/turbo/umms-maom/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/heterocyclic_nitriles_frag/`
- [x] docking finished
- [x] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## aldehyde-based-cyanoacrylamides
`/nfs/turbo/umms-maom/CovalentLibs/aldehyde-based-cyanoacrylamides/fragments/gz_files/
- moved `database.sdi` to `/nfs/turbo/umms-maom/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/aldehyde_based_cyanoacrylamides_frag`
- [x] docking finished
- [x] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## alkyl-halides
`/nfs/turbo/umms-maom/CovalentLibs/alykl-halides/fragments/gz_files/`
- moved `database.sdi` to `/nfs/turbo/umms-maom/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/alkyl_halides_frag`
- [x] docking finished
- [x] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)

## di-amine-linkers
- [ ] ligand prep
- [ ] db2.gz tldr
- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## fluorosulphones
- [ ] ligand prep
- [ ] db2.gz tldr
- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## amines
- [ ] ligand prep
- [ ] db2.gz tldr
- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## cyanamides
- [ ] ligand prep
- [ ] db2.gz tldr
- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## vinyl-sulfone
- [ ] ligand prep
- [ ] db2.gz tldr
- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)
## fmk
- [ ] ligand prep
- [ ] db2.gz tldr
- [ ] docking finished
- [ ] poses.mol2 made
- [ ] filter hits (first pass)
- [ ] filter hits (final pass)

