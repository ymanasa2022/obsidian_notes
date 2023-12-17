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
$DOCKBASE/ligand/generate/build_database_ligand.sh

$DOCKBASE/ligand/generate/build_smiles_ligand.sh smiles.ism --covalent 
- makes db2 from the smiles 
	- takes in smiles
	- generates solvation
	- combines to make db2

 $DOCKBASE/ligand/omega/omega_warhead.py 
 - run 264084.0.O.mol2 with omega_warhead.py and then follow subsequent lines in $DOCKBASE/ligand/generate/build_smiles_ligand.sh and run them one at a time on the mol2
- ~/turbo/opt/DOCK-dev/ucsfdock/ligand/generate/build_ligand_mol2.sh
	- takes mol2 
	- does stuff with omega 
	- combines to make db2
	- doesnt handle covalent but we can modify it to run covalent 


