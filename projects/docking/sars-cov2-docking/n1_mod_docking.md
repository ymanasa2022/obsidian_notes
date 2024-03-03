- synthetic chemists believe the N3 modifications will be hard to synthesize 
- must dock n1 mod ligands to sars cov2 rdrp 
![[gdp_structure.png]]
- want to keep the nitrogen atom on position N1 and add growing chains on that 
## Small scale docking 
- each ligand would need to be prepped 
- follow receptor and ligand prep instructions here: 
https://ringo.ams.stonybrook.edu/index.php/2021_DOCK_tutorial_3_with_PDBID_1S19
https://wiki.docking.org/index.php?title=SUBDOCK_DOCK3.8#Full_Example_-_All_Steps

### Choose a target pdb + target residue
- pdb 7CYQ
- on jarvis:  ssh ymanasa@jarvis.med.umich.edu
	- `/corexfs/ymanasa/lig1-prot/pflab-gdp-plig-prot`
	- `setup-prot-gdp-plig.pdb` was made using chainA,B,C,D,GDP from 7CYQ 
		- has hydrogens 
	- might be used for docking ![[sars_cov2_gdp_pymol.png]]
	- purple residue (Residue R 116 interacts with GDP)

### Make pdb files for ligands
![[original_ms_ligands.png]]
#### use vmd to visualize ligands 
- load 7CYQ.pdb into vmd
- Graphics -> Representations
- Selected Atoms -> resname GDP -> Coloring Method -> Element -> Drawing Method -> Bonds
- Create Rep -> Selected Atoms -> resname chain A -> Coloring -> Name -> Drawing -> NewCartoon 
- Create Rep -> Selected Atoms -> chain A and within 10 of rename GDP -> Color -> Element -> Draw -> Lines 
- Create Rep -> Selected Atoms -> resname LYS -> ColorID -> 1 -> Draw -> Lines 
- Can see that LYS 41 can interact with long chain from N1 on GDP 
- '1' to label atoms 
![[lys41_gdp_sars.png]]
##### use molefacture to visualize new ligands
1. Mods tested using FEP at N3 but now at N1 (Figure 9a): 
![[mod_fig9a.png]]
2. Novel modified ligand of Figure9
![[new_mod_fig9.png]]
3. Modified ligand from Figure 9e
![[figures/mod_fig9e.png]]
4. Modified ligand from Figure 9c 
![[mod_fig9c.png]]
5. Hybrid of figure9b and c 
![[mod_fig9b_c.png]]

6. Modified Figure 9d
![[mod_fig9d.png]]

Final Ligands: 
![[fig9_modified_ligs.png]]
### Make db2 files using tldr 
#### SMILES:
| ***mol_name*** | ***SMILES*** |
| ---- | ---- |
| gdp | OC1C(O)C(OP(O)(OP(O)(O)=O)=O)OC1N2C(N=C(N)NC3=O)=C3N=C2 |
| mod_fig9a | OC1C(O)C(OP(O)(OP(O)(O)=O)=O)OC1N2C(N=C(N)N(CCCCC([O-])=O)C3=O)=C3N=C2 |
| mod_fig9a_B | OC1C(O)C(OP(O)(OP(O)(O)=O)=O)OC1N2C(N=C(N)N(CCC([O-])=O)C3=O)=C3N=C2 |
| new_mod_fig9 | OC1C(O)C(OP(O)(OP(O)(O)=O)=O)OC1N2C(N=C(N)N(CCCCC([O-])=O)C3=O)=C3C(CCCCCC([O-])=O)=C2 |
| mod_figc | OC1C(O)C(OP(O)(OP(O)(O)=O)=O)OC1N2C(N=C(N)NC3=O)=C3C(CCCCCC([O-])=O)=C2 |
| mod_fig9e | OC1C(O)C(OP(O)(OP(O)(O)=O)=O)OC1N2C(N=C(CCCC)N(CCCCC([O-])=O)C3=O)=C3C(CCCCCC([O-])=O)=C2 |
| mod_fig9d | OC1C(O)C(OP(O)(OP(O)(O)=O)=O)OC1N2C(N=C(CCCC)N(CCCCC([O-])=O)C3=O)=C3N=C2 |
local: modified_smiles.smi
#### tldr for db2 generation 
![[figures/tldr_mod_ligs.png]]
![[tldr_mod_ligs.png]]
### Prep receptor
- using original pdb: 
	- 7CYQ 
	- rec.pdb is just chain A 
	- xtal-lig.pdb is GDP from chain A1003
- changed the INDOCK parameters 
- Make sure the vdw mesh was created in the right place
	- run `python2  /home/ymanasa/opt/dock_campaign_template/scripts/create_VDW_DX.py` in `dockfiles/` in `prepared_structures/` 
	- mesh looks like it's covering the right area (where gdp used to reside)
	- cyan part is just rec.pdb and does not include the ligand 
	- ![[sars_rdrp_vdw_mesh.png]]
### Dock using DOCK3.8 non-covalent 
`/home/ymanasa/turbo/projects/SARS-CoV-2/docking_runs/7cyq_20240104,manasas_ligs,,20240104`
- make sure INDOCK in prepared_structure/ dir has clashes off 
- poses of all docked poses: `poses.mol2`
- Here are the total energy values for the ligands 
![[total_energies_n1_mod_ligs.png]]
BUT, 
upon looking at the poses selected for each ligand, it seems like the ligands are not in the right orientation. 
Original GDP: ![[original_gdp.png]]
DOCK3.8 gdp docked: 
![[gdp_dock3.8.png]]
- could be insufficient ligand orientation sampling (tldr gives confirmations)
- could be incorrect assessment of docking by DOCK3.8
### Using DiffDock 
- using [DiffDock](https://colab.research.google.com/drive/1CTtUGg05-2MtlWmfJhqzLTtkDDaxCDOQ#scrollTo=ZAH5NYgIWIlI) instead to dock 
	- OC1C(O)C(OP(O)(OP(O)(O)=O)=O)OC1N2C(N=C(N)N(CCCCC([O-])=O)C3=O)=C3N=C2	mod_fig9a 
	- made some edits to collab notebook to get the top 30 hit results as a zip: 
		- first ranked pose: ![[collab_modfig9a_diffdock.png]]
		- the pyrophosphate group is hanging out of the active site rather than being buried in the pocket  
		- the ribose ring is not interacting with the histadine either 
			- to make sure that the interaction between the ribose ring plus histadine and the long carboxyl chain plus the LYS41:
				- change mouse mod (right down) to 3-button editing
				- select atoms and rotate using shift/ctrl 
