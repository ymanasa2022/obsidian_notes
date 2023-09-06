Working on organizing data into [TgCPL Activities](https://docs.google.com/spreadsheets/d/1Lo0Nc6OFRyUe0arYsGTmi4eR1rFFTiq_GEcoAIC9rmE/edit?usp=sharing) from [experimental data](https://docs.google.com/spreadsheets/d/0B7YNPpJXYWK8cnFVWXFxMWJhZDV4dmM3LVZvNmFldDlCbTJV/edit?usp=sharing&ouid=104609175179432674295&resourcekey=0-q9aMd3mjCopFToB8Kx_lEA&rtpof=true&sd=true)

Project outline (from [[bender_2021]]):
1. Retrospective test:
	- assess current docking model with known experimentally docked ligands to TgCPL
		- [ ] involves creating a data set with experimentally docked ligands and their binding efficiency values 
		- [ ] having the structures of these docked ligands to the protein target 
		- [ ] docking these known ligands to the protein target
		- [ ] assessing rmsd values of docked vs experimentally determined ligand+protein complexes
	- Tweak docking model 
		- [ ] calibrate scoring functions 
			- [ ]  https://chemrxiv.org/engage/chemrxiv/article-details/64c99291658ec5f7e5947f03 
		- [ ] use an extrema set (decoys/inactive ligands related to the active ligands--property match decoys) to evaluate
			- [ ] asses using decoy discrimination tests 
			- [ ] tldr to create decoys; does a property similarity search but chemically different. DUD-E also does this. 
2. Covalently Dock: 
	- use method to dock a library of commercially available ligand types assessed in previous step
		- [ ] make library using guide to pharmacology.com, chemb, pubchem, binding db
			- one zinc id might correspond to different chmbl molecules. toxoplasma cpl and human cpL
			- [ ] take out ones with low pChEMBL Values and ones with comments in data validity. repeat for human cpl
				- pChEMBL allows comparable measures of half-maximal response concentration/potency/affinity to be compared to a negative logarithmic scale. an IC50 measurement of 1nM would have a pChEMBL value of 9. pChEMBL = -log(molar IC50, XC50, EC50, AC50, Ki, Kd or Potency). Higher the better?
	- assess top-ranked x% of the library 
	- purchase highest/medium ranked compounds and lowest ranked compounds similar to higher ranked commercially unavailable compounds 
3. Get co-crystal compounds of the most promising new ligands 
	- validate docking poses for highest ranked ligands
		- [ ] RMSD
4. experimentally test inhibition of protein by new ligands 
	- IC50
	- MIC
	- activity assays
	- full dose-response curves against protein target

look at grant for steps 
https://pubs.acs.org/doi/full/10.1021/jacs.9b10377
