`/home/ymanasa/turbo/CovalentLibs/martin_cdd/martin_cdd_09132023`.ism
- created a `.ism` file with SMILES given by Martin on Sep 13, 2023 (also in CDD Vault)
- example `.ism`:  `/home/ymanasa/turbo/CovalentLibs/unsubstituted-acrylamides/fragments/smiles/unsub.frag.acrylamides.ism`
- script to run for `Si` replacement: `/home/ymanasa/turbo/CovalentLibs/scripts/unsat-ab-carbonyl.py`
- created `martin_cdd_09132023.ism` in `/home/ymanasa/turbo/CovalentLibs/martin_cdd`
	- used columns C D to create tab spaced file `martin_cdd_09132023.ism` 
	- use one of the `heterocyclic-nitrile.py` files to convert the nitril groups in all the SMILES in `martin_cdd_09132023.ism`
	- look at line 19 SMIRKS reaction in smarts.plus 
![[heterocyclic-nitril.png]]
![[heterocyclic-nitril-1.png]]
![[heterocyclic-nitrile-2.png]]
![[heterocyclic-nitrile-3.png]]

- in conda environment `docking` , I installed openeye tools using: 
	`conda config --add channels openeye`
	`conda install openeye-toolkits`
