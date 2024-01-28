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
