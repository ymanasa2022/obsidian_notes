need ligands experimentally docked to toxoplasma cpl and human cpL 
chembl will give a curated list of ligands that were experimentally tested against given receptors

- TgCPL Organism: CHEMBL612888
- HsCPL Organism: CHEMBL3837

[Latest version](https://docs.google.com/spreadsheets/d/1Lo0Nc6OFRyUe0arYsGTmi4eR1rFFTiq_GEcoAIC9rmE/edit?usp=sharing)
[Local Versions]/Users/ymanasa/Library/CloudStorage/OneDrive-MichiganMedicine/1PhD/omeara_lab/TgCPL/Data/ligand\ activites/TgCPL_\ CHEMBL612888_ligand_activities.xls 

- Criteria for filtering lists. deleted rows if they had: 
	- Low or NO pChEMBL Values (anything less than 4)
		(pChEMBL allows comparable measures of half-maximal response concentration/potency/affinity to be compared to a negative logarithmic scale. an IC50 measurement of 1nM would have a pChEMBL value of 9. pChEMBL = -log(molar IC50, XC50, EC50, AC50, Ki, Kd or Potency) Higher the better)
		
	- Data Validity Column has "ND" or "Not Determined" or "Not active" or "Not Evaluated" or "outside normal range" or "active"-- and doesnt have pchembl or standard value info 
	
	- Standard Value and Stander Unit Columns that have values greater than 1000nM. (anything greater than 1mM doesn't reflect biological accuracy. anything that is given as a percentage was also taken out. kept mg.kg-1 and other units as long as it was the right standard type)
	
	- Standard Type column with "Survival" or "Inhibition" or "mortality" or "activity" or "ratio"
		- keeping "inhibition" lines if reported in nM
		- in vivo: "assay organism" must be Toxoplasma Gondii or Homo Sapiens
	
	- All cells with no data have 'None' now