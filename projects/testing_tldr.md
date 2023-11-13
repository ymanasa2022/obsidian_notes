# Rebuild Ketone Based Enones
- rebuilding a subset of enamine ketone_based_enones using ***build3d_dock38***
	- the enamine libraries might have older formats of the db2 files that are not compatible with dock3.8
	- the output gz file from tldr seems incomplete 
		- there's only a few db2 files and doesn't seem to be more than one molecule per db2 file  
	- database will be here: `/nfs/turbo/umms-maom/CovalentLibs/partial_ketone_enone_dock38test`
- also rebuilt same subset using mol2 file (from Miguel) ***build3d_mol2***
	- want to check whether output has same missing molecules or not

# Testing Non-Covalent Dock3.8
- test non-covalent docking with partial ketone covalent library dock3.8 

# Testing Covalent Dock3.8
- test covalent docking with partial ketone covalent library dock3.8 