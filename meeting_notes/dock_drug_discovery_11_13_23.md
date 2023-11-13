# SARS-CoV2 covalent docking mechanism  
- covalent docking mechanism 
- residues in the active site currently used as a target for drugs 
- known resistance (mutations in the active site)
- preferred substrate conformation 
- crystal structure of mutant structures differences 
- types of interactions the catalytic backbone amino acids or mutations have with residues/chains around it 

# Scoring fnx based on grid free energy model in protein-ligand interaction 
- issues with dock3.7 scoring function. doesn't consider:
	- receptor flexibility (only rigid receptor docking)
	- entropy(none)
	- ligand desolvation 
	- target desolvation 
- SILCS: originally used to find potential ligand bonding site 
	- can capture protein side chain movement 
	- MC and MD simulation used to find all conformations 
	- protein is placed in a water box 
	- fragments compete with water molecules and affinity is computed using LGFE in SILCS simulation
- LGFE was introduced into DOCK3.7 to optimize the scoring function 
- problem: figuring out what types of fragments or how many fragments to use to develop the scoring function 