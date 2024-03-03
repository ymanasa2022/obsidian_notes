!! conda env: ***docking***
# Nov 28, 2023 
## DOCK3.8 not working
- issue with db2.gz file format 
- having issues with reading the tar file format 
- used one of Miguel's tar files and ran into `tarfile.ReadError: invalid header` 
- ReadError being raised 
- [_exception_ `tarfile.ReadError`](https://python.readthedocs.io/en/latest/library/tarfile.html#tarfile.ReadError "Permalink to this definition")
	- Is raised when a tar archive is opened, that either cannot be handled by the [`tarfile`](https://python.readthedocs.io/en/latest/library/tarfile.html#module-tarfile "tarfile: Read and write tar-format archive files.") module or is somehow invalid.
- encodings in the number field seem to be the issue?
![[invalidheader_dock38.png]]

- Attempt to print out contents of the [tar file](https://unix.stackexchange.com/questions/208482/view-a-file-in-a-tar-archive-without-extracting-it)
- tar reads and writes [headers](https://www.ibm.com/docs/en/zos/2.1.0?topic=formats-tar-format-tar-archives) in either of the original TAR format or from UNIX systems 
	- this might be causing an issue with reading the header
- Tested with Marissa's db2.gz file (on tgcpl_20231115 non covalent docking)
	- it didn't work; same invalid header error 
	tar: This does not look like a tar archive
	tar: Skipping to next header
	tar: Exiting with failure status due to previous error
	- must figure out what file it is trying to untar 
	- it is untarring the db2.gz file and running into a parsing error in the first few lines of the unzipped file ![[untar_parse_error.png]]![[untar_file_=cc(=o.png]]
- copied dock_submit.sh from $DOCK_TEMPLATE
	- made these changes
	![[dock_submit_changes.png]]
	- change the path to dock_submit.sh in the 1_submit.sh script created for each dock run 

# Debugging with Matt Dec 14, 2023 
- using python debugger (pdb)
	- python -m pdb myscript.py 
	
- $DOCKBASE/ligand/generate/build_database_ligand.sh
- $DOCKBASE/ligand/generate/build_smiles_ligand.sh smiles.ism --covalent 
	- makes db2 from the smiles 
	- takes in smiles
	- generates solvation
	- combines to make db2
## continued Jan 02, 2024
 - $DOCKBASE/ligand/omega/omega_warhead.py -> works with /home/ymanasa/turbo/projects/TgCPL/maom_covalent_test/databases/martin09132023_cdd/archive/build3d38/gz_files/1/264084.0.O.mol2 with omega_warhead.py
	 - creates a db2in.mol2 file in same gz_files directory 
 - $DOCKBASE/ligand/generate/build_smiles_ligand.sh 
	 - run them one at a time on the mol2
	 - need Marvin suite and licensing 
- ~/turbo/opt/DOCK-debug/ucsfdock/ligand/generate/build_ligand_mol2.sh
	- takes mol2 
	- does stuff with omega 
	- combines to make db2
	- doesnt handle covalent but we can modify it to run covalent (line 20 runs omega noncovalent script)

## continued Jan 22, 2024
- start: source setup_dock_environment_3.8_debug.sh in maom_covalent_test
- 1 docking_run: 1_submit.sh runs `${DOCK_TEMPLATE}/scripts/dock_submit.sh`
- 2 dock_submit.sh runs `${DOCKBASE}/docking/submit/subdock.bash`
- 3 subdock.bash runs `${DOCKBASE}/docking/submit/rundock.bash`
-----
- omega_warhead.py is use to create db2in.mol2 files for each SMILES using mol2 file in gz_files
- generate protomers using something other than Marvin (ChemAxon) in `build_smiles_ligand.sh` (SMILES file required) -> then runs omega_warhead.py on generated protomers (mol2 input required)
 - IF we want protomers for martin's ligands specifically: /home/ymanasa/turbo/projects/TgCPL/maom_covalent_test/databases/martin09132023_cdd/smiles 
	 - testing with https://github.com/forlilab/scrubber/
	 - wrote script: `/home/ymanasa/turbo/opt/DOCK-debug/ucsfdock/ligand/generate/build_smiles_scrubber.py`
	 - can also try with command line: `scrub.py "CC(C)n1cnc2c1nc(nc2C(=[N])[SiH3])N(Cc3ccc(cc3)F)CC4CCCC4" -o scrubbed.sdf`
	 - but we need a mol2 file to input into omega_warhead.py
	 ![[output_protonated_state_scrubber.png]]
	- before omega_warhead.py is $DOCKBASE/ligand/amsol/calc_solvation.csh which needs a mol2 input AFTER protomers states are computed using [scrubber]( https://github.com/forlilab/scrubber/)
#### Summary
- build_smiles_ligand.sh: run on a set of smiles 
	- generates protomer states using *Marvin ChemAxon*, output: .smi 
	- *molconvert* embed SMILES in 3D + add hydrogens to each protomer, output: .mol2
	- *calc_solvation.csh* on mol2 protomer/protonated states, output: output.mol2
	- *omega_warhead.py* uses output.mol2 to create various conformations, output: db2in.mol2 files
	
- Trying to make this instead in `build_smiles_ligand_scrubber.sh`: 
	- generate protomer states using *Scrubber*, output: .smi 
		- wrote `$DOCKBASE/ligand/protonate/prot_scrubber.py`
		- needs to process multiple SMILES 
		- replaces `"$LINE" | $DOCKBASE/ligand/protonate/prot_marvin.py -H $PH -d $DOMAIN_CUTOFF -o $NAME-protonated.ism`
	- embed SMILES in 3D and add hydrogens using *OpenBabel*/*rdkit*? output: .mol2
	- still use *calc_solvation.csv* 
	- still use *omega_warhead.py* 

## continued Jan 24, 2024
- attempting to just use `/nfs/turbo/umms-maom/opt/scrubber/scripts/scrub.py` to get protomers as well as embedded SMILES in 3D
	- `scrub.py /home/ymanasa/turbo/projects/TgCPL/maom_covalent_test/databases/martin09132023_cdd/smiles/martin_cdd_09132023.smi -o martin_cdd.sdf` 
	- at ph 7.4
	- gives sdf file 
	- generates embedded SMILES in 3D as well (can skip using --skip_gen3d flag)
	- generates using RDKit's ETKDGv3 and UFF minimization
- can skip embedded SMILES in 3D step (since scrubber does it using rdkit)
- updated code in `build_smiles_ligand_scrubber.sh`
#### Summary Update
- Trying to use scrubbed instead of any ChemAxon steps in `build_smiles_ligand_scrubber.sh`: 
	- generate protomer states using *Scrubber*, output: .sdf 
		- replaces `"$LINE" | $DOCKBASE/ligand/protonate/prot_marvin.py -H $PH -d $DOMAIN_CUTOFF -o $NAME-protonated.ism`
		- makes a directory for each ligand 
	- embed SMILES in 3D and add hydrogens using *OpenBabel*/*rdkit*? output: .mol2
		- need to replace this step with sdf -> mol2 conversion using OpenBabel
	- still use *calc_solvation.csv* 
	- still use *omega_warhead.py* 
## continued Jan 26, 2024
- `build_smiles_ligand_scrubber.sh`: 
	- generate protomer states using *Scrubber*, output: .smi
		- makes a directory for each ligand: `ligand/generate/JRH-10-3P/
		- might want to pass each SMILES and get a SMILES output 
			- doing this using `/nfs/turbo/umms-maom/opt/scrubber/scripts/scrub_smi.py` within `build_smiles_ligand_scrubber.sh`
			- writes a file with SMILES protomers (smi) 
			- ![[output_scrubber_protomers.png]]
			- `bash build_smiles_ligand_scrubber.sh martin_cdd_small.smi --covalent /nfs/turbo/umms-maom/opt`

FC1=CC=C(CN(CC2CCCC2)C2=NC(C#N)=C3N=CN(C(C)C)C3=N2)C=C1 JRH-10-3P
FC1=CC=C(CN(CC(C)C)C2=NC(C#N)=C3N=CN(C(C)C)C3=N2)C=C1   JRH-9-100P
FC1=CC=C(CN(CCC(C)C)C2=NC(C#N)=C3N=CN(C(C)C)C3=N2)C=C1  JRH-10-1P

- embed SMILES in 3D and add hydrogens using *RDKit* output: .mol2
	- replace this step with SMILES -> mol2 conversion using RDKit 
	- wrote python script in `/ligang/rdkit/mol_from_smiles.py` that uses `rdkit.Chem.MolFromSmiles("SMILES")` and `Chem.AddHs(mol) `to add Hs and embed SMILES in 3d as mol2 file 
	- still use *calc_solvation.csv* 
	![[calc_solvation_error.png]]
	https://open-babel.readthedocs.io/en/latest/Installation/install.html
	`make install` step
	![[openbabel_compiler_err.png]]
	- still use *omega_warhead.py* 
- smiles to mopin (using obabel)
	- or write to sdf to mopin 

## continued Jan 30, 2024
- in theory we should be able to just run tldr output files through omega_warhead.py script 
	- need to check if .solv file from tldr is same output from calc_solvation.csh that is run on the protomer mol2 file for each protein 
	- martin's tldr output: `/nfs/turbo/umms-maom/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/martin09132023_cdd_new/archive/build3d38/gz_files/1`
	- output.mol2 is from `calc_solvation.csh`
	- `csh calc_solvation.csh /nfs/turbo/umms-maom/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/martin09132023_cdd_new/archive/build3d38/gz_files/1/JRH-10-3P.0.N.mol2 `
	![[obabel_solvation_error.png]]
	- `ldd /home/ymanasa/turbo/opt/bin/obabel`to list library dependencies of obabel
	- in calc_solvation.csh they suggest setting DOCKBASE and OBABELBASE in ~/.bashrc
		- added: 
		`export OBABELBASE=${HOME}/opt/build`
		`export DOCKBASE=${HOME}/turbo/opt/DOCK-debug/ucsfdock`
## continued Jan 31, 2024
- need to reinstall openbabel in a place I have write permissions 
- Matt: To install obabel with out admin privileges, you need to specify where you want to install it--somewhere that you have write access. E.g. I put a copy in ~/turbo/opt, but you could put your own copy in `~ymanasa/opt` . To do this when you would do,    
>`cmake ../openbabel-openbabel-2-4-0 -DCMAKE_INSTALL_PREFIX=/home/ymanasa/opt `
  `make`  
  `make install`
- [install openbabel ](https://open-babel.readthedocs.io/en/latest/Installation/install.html)
- in `/home/ymanasa/opt/build` 
- testing calc_solvation.csh on mol2 from tldr martin's compounds: 
> `csh calc_solvation.csh /nfs/turbo/umms-maom/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/martin09132023_cdd_new/archive/build3d38/gz_files/1/JRH-10-3P.0.N.mol2`
![[obabel_ZmatMOPAC_error.png]]
- testing obabel mol2 to MOPAC conversion:
> `/home/ymanasa/opt/build/bin/obabel -i mol2 temp.mol2 -o mopin -O /home/ymanasa/turbo/opt/DOCK-debug/ucsfdock/ligand/amsol/temp.ZmatMOPAC`
- the library it was using was in turbo not through my build 
	- added to `.bashrc`: `export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:${HOME}/opt/build/lib`
	- convertion from mol2 to ZmatMOPAC works (line 92 in calc_solvation.csh)
- AMSOL
`ldd /home/ymanasa/turbo/opt/amsol/amsol7.1/amsol7.1.exe`
## continued Feb 2, 2024
- line 106 in calc_solvation.csh 
	- works (output: temp.in-wat, temp.in-hex)
- line 111 `timeout $amsoltlimit $SHELL -c "$AMSOLEXE < temp.in-wat > temp.o-wat"`
	- runs amsol.exe (`amsol7.1`)
	- amsol calculates the change in energy when molecules are dissolved in water or an organic solvent. might be also used to calculate partition coefficients and their logarithms (Log P) which tells solubility of a compound.
	- setting AMSOLEXE in setup_env script may not be the right way to do it 
		- can just use `amsol7.1` within `$DOCKBASE/ligand/amsol/amsol7.1`
		- set amsoltlimit = 1m and AMSOLEXE = `/home/ymanasa/turbo/opt/DOCK-debug/ucsfdock/ligand/amsol/amsol7.1`
		- error with loading shared lib libg2c.so.0
![[amsol_error.png]]
`ldd /home/ymanasa/turbo/opt/DOCK-debug/ucsfdock/ligand/amsol`
![[amsol_libraries.png]]
- moved amsol to /home/ymanasa/opt 
	- upon reading README.md: `module load pgi/20.4` and `patch port/intcar.f ${DOCKBASE}/ligand/amsol/patches/amsol7.1_port_intcar.f.diff`
		- added module load into bachrc 
	- set AMSOLEXE path in setup env script
	- rerunning line 111 works now! 
	- line 130 also works! 
- testing calc_solvation.csh on a tldr output: 
	- `csh calc_solvation.csh /nfs/turbo/umms-maom/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/martin09132023_cdd_new/archive/build3d38/gz_files/1/JRH-10-3P.0.N.mol2`
	- works ; output:temp files (incl temp.mol2)
- testing omega_warhead.py on temp.mol2 
	- `python ../omega/omega_warhead.py temp.mol2 `
	- output: `temp.1.db2in.mol2` example in `$DOCKBASE/ligand/amsol/calc_sol_out`
## continued Feb 4, 2024
- need to pass in all $PROT_NAME.mol2 files into calc_solvation.csh  and then into omega_warhead.py.. etc etc to get 
- testing if the conversion from `temp.1.db2in.mol2` works 
	- line 71
	- `$DOCKBASE/ligand/mol2db2/mol2db2.py -v --covalent --mol2=temp.1.db2in.mol2 --solv=output.solv --db=$onemol.db2.gz`
	- ![[db2_converstion_gz.png]]
- `"-n", "--namemol2", type="string", action="store", dest="namefile"` in is being set incorrectly in mol2db2.py ?? 
	- not sure what this name.txt file is 
	- {'verbose'....} in above fig shows arguments of mol2db2.py being used in mol2.py
	- fixed: need to run prepare.py as well as VERBOSE lines in `$DOCKBASE/ligand/amsol/process_amsol_mol2.py3.py` lines were changed 
- `$DOCKBASE/ligand/mol2db/mol2db $DOCKBASE/ligand/mol2db/data/inhie` combines .mol2 and .solv file to create .db2 file
	- where does solv file come from????
	- tried combining JRH-10-3P.0.N.solv and JRH-10-3P.0.N.mol2 
		`/nfs/turbo/umms-maom/projects/TgCPL/maom_covalent_test/databases/martin09132023_cdd/archive/build3d38/gz_files/1`
	- rename files to db.mol2 and mol.solv and run line 104 from` build_smiles_ligand.sh` in directory with these 
	[detached from 4173476.pts-105.gl-login1]
## continued Feb 5, 2024 
- run prepare.py on mol2 from tldr output -> `name.txt`
- run omega_warhead.py on mol2 -> `*.db2in.mol2`
- run mol2db2.py on db2in.mol2 -> `*.db2` (written as .db2.gz but isnt zipped)
- lines 80 onwards in `build_smiles_ligand.sh` is for DB generation which is no longer used
	- instead tar + zip each `.db2` file `tar -czvf *.db2`
	- untar+unzip: `tar -xzvf`
- `tarstream` python error while docking issue
	- tar+zip the output from `mol2db.py` manually 
- can dock with covalent dock3.8 with these tgz files 

- `build_ligand_tldr.sh`: takes in path to zip tldr results (build3d38) and cov/non-cov
	- unzip
	- go into `*_build3d38/`
	- for each num/ do;
		- `tar -xvf 1.tar.gz`
		- `cd 1/`
		- for loop through all `*.mol2` files 
			- rest of steps in `build_ligand_smiles.sh` for each mol2 from prepare.py, skip calc_solvation.csh, then omega_warhead.py, finally mol2db2.py, tar+zip
## continued Feb 6, 2024 
- wrote` build_ligand_tldr.sh`script 
- takes path to zipped tldr output 
- unzips
	- prepares name.txt for each protomer
	- runs omega_warhead on each, gives mol2
	- runs mol2db2.py on each, gives db2
	- tgz each db2 file 
## works as of Feb 7, 2024
- tested on small.zip 
- able to run on all Martin ligands 
within conda env docking:
> `sh /home/ymanasa/turbo/opt/DOCK-debug/ucsfdock/ligand/generate/build_ligand_tldr.sh build3d38_results.zip --covalent`
should give us all the `db2.tgz` files needed for dock3.8 to dock martin's ligands 

`/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/martin09132023_cdd_new/archive/build3d38/build3d38_results/`
## DOCK3.8 on Martin's CDD ligands
##### Feb 8, 2024
- all db2.tgz files are in /`home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/martin09132023_cdd/`
- moved setup debug script to my dock campaign dir 
- database.sdi in `martin09132023_cdd/` points to all .db2.tgz files for all molecules from tldr
	- these .db2.tgz files were made using `/home/ymanasa/turbo/opt/DOCK-debug/ucsfdock/ligand/generate/build_ligand_tldr.sh` (look above)

... continued in [[docking_martin09132023_tgcpl]]

## Feb 8, 2024 
### Docking run to TgCPL using db2.tgz generated files
- noticed that a lot of the OUTDOCK.0 files had the same molecule (JRH-9-100P)
- also a lot of the OUTDOCK's showed errors due to broken lines (included JRH-9-100P)
- rerunning docking with smaller set of db2.tgz that doesnt include JRH-9-100P 
	- this molecule still showed up in `OUTDOCK.0` file!?
	- only three lines in db2.tgz but 4 directories were created after docking??
- noticed that when i run `omega_warhead.py` from `DOCK38` instead of `DOCK-debug` on the mol2 file, there were errors; maybe there are other scripts i fixed in DOCK-debug ?
- testing docking of only `JRH-9-100P.0.N.db2.tgz` generated by scripts in `DOCK-debug/ucsfdock/`
	![[debugging_statements.png]]
- testing only with `JRH-9-100P.0.N.db2.tgz` with `DOCK38/ucsfdock/`
	- doesn't work 
 - USE DOCK-debug in DOCKBASE for non docking part
 - USE DOCK38 for docking
#### Next step issue: gathering poses 
- testing on results in `archive/hscpl_5MAJ_20231023,aldehyde_based_cyanoacrylamides_frag,,20231031`
- seems to work fine if results arent weird 
## Feb 9, 2024
### docking using generated db2 and DOCK38
- mol2db2.py generates a db2.gz file that needs to FIRST be UNZIPPED to get a db2 file
- THEN this db2 file needs to be tar+zipped 
- THEN path to this db2.tgz needs to be in database.sdi for DOCK38

- remove D lines from db2.gz unziped files and then re-tar.gz
- make sure name.txt files are being made for each PROT_NAME file before tzg step 

## Feb 10, 2024
- refer to `/home/ymanasa/turbo/opt/DOCK-debug/ucsfdock/ligand/generate/build_ligand_tldr.sh`
- made changes listed above
- generated db2.tgz files for dock38 docking (`/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/martin09132023_cdd`)
- now continue with docking [[docking_martin09132023_tgcpl]]

## Feb 12, 2024
- trying to use gz files for docking instead of tgz 
- testing dock38 covalent on .db2.gz files from tldr as well as after conversion through my script
- these are the ones that are directly from tldr:
>build3d38_results_small/1/JRH-9-100P.0.N.db2.gz
  build3d38_results_small/1/JRH-10-3P.0.N.db2.gz
  build3d38_results_small/1/JRH-10-1P.0.N.db2.gz
  build3d38_results_small/1/380148.0.N.db2.gz
  build3d38_results_small/1/380147.0.O.db2.gz
  - the rest dont have D blocks and were gzipped again 
  - the ones that were unprocessed from tldr did not work for sure
  - some of the processed ones worked: 264183.0.N and didn't: 263022.0.N
  - i didnt put gzip statement in right place... doing it agian...

- want to test:
	- Processed with my script & D block  (have to run these separately because of naming convention)
		- 264084.0.O.D.db2.gz
		- 264183.0.N.D.db2.gz
		- 265367.0.N.D.db2.gz
		- Error: 264084.0.O BrokenD line; the rest were ok 
- ran these together:
	- Processed with my script & no D block 
		- 264084.0.O.db2.gz
		- 264183.0.N.db2.gz
		- 265367.0.N.db2.gz
		- Error: None 
	- Not processed wtih my script (from tldr) & no D block 
		- JRH-10-1P.0.N.db2.gz
		- 380148.0.N.db2.gz
		- 380147.0.O.db2.gz
		- Error: does not contain covalent colored atoms
### db2.gz for martin's ligs
- all smiles and ccg# from tgcpl_activities
- add Si using `/home/ymanasa/turbo/CovalentLibs/scripts/heterocyclic-nitrile-1-py3.py`
- using `/home/ymanasa/turbo/projects/TgCPL/docking-campaigns/docking_campaigns_local/databases/martin09132023_cdd/smiles/diff.py` found that 87 compounds from original list are not being converted?? and some are being written twice to output.ism
	- heterocyclic script does not convert SMILES that dont have a:3 in it
	- need to rewrite SMARTS pattern to do reaction for SMILES that have C:2,N:3 instead of aromatic atoms 
- still docking whatever compounds I have using dock38 and tldr build3d38 output 
	- some ligands work and some give ligand covalent colored atoms error
	- traced back to `/home/ymanasa/turbo/opt/DOCK38/ucsfdock/docking/DOCK/src/cov_search.f`

[Summary to Matt for continued debugging](https://docs.google.com/document/d/1VHRNiJANUeBIUqtE9mhtRpdaASDP01bRnpHlBztl5VI/edit)
