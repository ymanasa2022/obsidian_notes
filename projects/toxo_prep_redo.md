# Choosing structures
Need to use the aligned tgcpl to hscpl pdb file 
use the hscpl ligand coordinates from the aligned hscpl structure to make the xtal-lig file

- PDB for TgCPL: 3F75
- Choosing best PDB for HsCPL with bound ligand: 
	- chose from the ones i chose to dock to
	- 5MAJ and 3O1G have the best resolutions 
		- 5MAJ (cathepsin L) (1.00 Å): RMSD when aligned to 3F75 = 0.491
		- 3O1G (cathepsin K) (1.65 Å): RMSD when aligned to 3F75 = 0.609 
		- have to choose the lowest RMSD: ***5MAJ***			
# Ligand Prep
- Finding which residue the ligand in HsCPL would covalently bind to in TgCPL 
- Reside 31 CYS is where the covalent binding will occur 
- 7KH is ligand code
- ![[5MAJ_3F75_ligand_bound.png]]
- get the atom coordinates from the aligned HsCPL pdb from pymol 
	- after aligning HsCPL to TgCPL, select the Ligand (Residues Selecting-- from lower right corner)
		- File ->  Export Molecule -> Selection: (sele) -> change file extension to .pdb
			- this will be my ***xtal-lig.pdb*** file 
		- Reloaded the 7KH.pdb file with the TgCPL structure and noticed that the ligand from 5MAJ and 3F75 align well but there is of course no bond between the Cysteine in TgCPL and ligand
		![[5maj_ligand_in_tgcpl.png]]
# Structure Prep
- structure used for docking: 3F75.pdb -> rec.pdb
- ligand used for docking: 7KH.pdb -> xtal-lig.pdb 
- covalent docking to residue: 31 CYS 
![[tgcpl_cov_residue_contact.png]]

- manual prep: 
	- copied xtal-lig.pdb and 3F75.pdb into tgcpl_3F75_20231204/ on greatlakes 
- the receptor pdb was saved from the pymol session 
# Prepare Structure
- changed the following in first prep code:
COVALENT_RESIDUE_NUMBER=31
COVALENT_RESIDUE_NAME=CYS
COVALENT_RESIDUE_ATOMS=SG
(tried both HG and SG; neither worked-- should be HG)
- blastermaster did not work![[blastermaster_EDO_error.png]]![[EDO_rec_pdb.png]]
- 1,2-ETHANEDIOL is denoted as EDO in PDB and should be X as the one letter code 
- HETATM is applied to non standard protein residues such as substrates/ligands 
- these needed to be taken out in the structure step 
	- using a the 1_make_structure.sh script to continue structure prep 
	- this takes out any HETATM that don't belong to the receptor
- redoing it with HG since that's the atom that will be replaced in the covalent docking step
	- kinda confused tho because there is no HG in rec or lig
- blastermaster standard and blastermaster covalent worked 

 ## Sanity check
 python2 script create_VDW_DX.py to visualize vwd mesh  (vdw.dx)
 make sure it is in the right place
 >>>  python2 /home/ymanasa/opt/dock_campaign_template/scripts/create_VDW_DX.py
 saved as `tgcpl_3f75_mesh.pse`

![[vdw_mesh_tgcpl_blastermaster.png]]


# Docking Run
- moved all old files into archive/
- changed 
	- `bash ${DOCKBASE}/docking/submit/subdock.bash` in `1_submit.sh in docking_runs/structure/`
	- `export **DOCKEXEC=**${DOCKBASE}/docking/DOCK/dock64`
- docking the unsub acrylamides db
![[same_tar_error.png]]