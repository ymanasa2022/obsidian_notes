***Andreas Luttens:***
- during a drug campaign he found that while there were fragment hits, after using existing lead like compound libraries based on his fragment hit, there were no viable lead like hits 
	- limitations of the chemical space of lead like compounds 
- open source implementation of GDB
	- the input superstructure space is enumerated based on a set of rules to ensure generation of molecules can be synthesized 
	- to create lead like libraries from a fragment hit search campaign 
	- lead like compounds are functional group additions to the fragment hits 
		- Andreas' implementation adds bonds and atoms systematically to create various combinations and permutations of adding heavy atoms, bonds, etc 
		- creates unique chemical spaces from a fragment of interest 
- says starting with fragments reduces total theoretical compounds when in lead like chemical space 
- Andreas' implementation includes branching out from carbon atoms or other atoms of a fragment based on whether or not there would be new hydrogen bonds formed to the receptor 
	- optimization is done using existing physics optimizers (thin spheres)
- wet lab experiments: thermal and IC50 
- fragments get higher hit rates than lead like searches 

***Marissa Dolorfino:***
- creating database of receptor ligand interactions 
- foundation models to support large scale docking methods 
- training models require large datasets for language models 
	- training loss decreases when training tokens increase 
- ChemGPT 
- dont have structural data to train chemical models 
	- PDB, ChEMBL, PubChem, Reaxys (experimental data sets)
	- Quantum chemistry based data sets and synthetic datasets 