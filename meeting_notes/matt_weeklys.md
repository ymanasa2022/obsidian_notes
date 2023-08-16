A week is normally from Wednesday to Wednesday due to weekly one-on-ones
# Aug 14, 2023 (Mon)

## Things discussed 
1. To make the most of grad school
	- go to at least one seminar per week
	- go to ALL DCMB department events
	- go to at least one big conference per year 
2. NSF GRFP grant
	-  October 16th, 2023 deadline
	- Funds 3 years of research
	- Have a draft in a month (Sept 15 draft deadline).
3. BIDS-TP training grant
	- May 1st, 2024 deadline
4. Important Docking issues: in which situations will we need to get accurate simulations of these issues and which ones can we skip to speed up simulations/computations?
	- water modeling: might be done using diffusion models
	- receptor flexibility
	- handling metals, covalent interactions
	- quantum chemistry: orbits, charge transfer etc 
5. Future Directions:
	- targeting proteins with cofactors in Active Site or proteins with post translational modifications 
	- pre-training: clustering of info in interaction matrices of many receptors and ligands 
		- good clusters can be further refined using high resolution simulations 
		- lower quality clusters can be further investigated using computationally cheaper simulations
6. TgCPL 
	- creating a docking model to perform high through put screening of ligands against Toxo cathepsins 
	- model needs to perform well with existing ligands that have been experimentally docking to human cathepsin proteins in order to use it to predict ligand affinity to the Toxo Cathepsin 
	- curation of human cathepsin data is done in TgCPL activity sheet
7. Broader Qs plus goals
	- what are the controls, why are we testing, what are we testing, here's the baseline, what is the experiment, what did we find, what does this mean 
	- help biologists and chemistry to do docking themselves instead of needing an expert
	
## To do for the week
1. Administrative
	- [x] set up obsidian on macbook and ipad
	- [x] update calendar with grant dates
	- [x] go through onboarding doc 
		- [ ] get DOCK3.8 license 
	- [x] sign up for mentor mentee workshop 
	- [x] send itemized bill from apple
	- [x] add yourself to appropriate mailing lists
	- [x] share this github repo with Matt 
		- [x] need to change visibility of the repo. can't seem to figure that out yet.
	- [x] cancel apple macbook order
	- [ ] go to 1 seminar (Aug 18, Fri 10 am Protease in Action)
	- [x] get keys to building room
	- [ ] Training: Healthy Relationships
	
2. Readings
	- **TgCPL**
		- [x] [[pogorzelska_2018]] 
			[*Cysteine cathepsins as a prospective target for anticancer therapies—current progress and prospects*](https://pubmed.ncbi.nlm.nih.gov/29870804/)
		- [x] [Larson et al. 2009](larson_2009)
			[*Toxoplasma gondii Cathepsin L Is the Primary Target of the Invasion-inhibitory Compound Morpholinurea-leucyl-homophenyl-vinyl Sulfone Phenyl*](https://www.jbc.org/article/S0021-9258(20)38515-X/fulltext)
		- [ ] [Bender et al. 2021](bender_2021)
			[*A practical guide to large-scale docking*](https://www.nature.com/articles/s41596-021-00597-z](https://www.nature.com/articles/s41596-021-00597-z)
		- [ ] [London et al. 2014](https://pubmed.ncbi.nlm.nih.gov/25344815/)
			*Covalent docking of large libraries for the discovery of chemical probes*
	- **Active ML Docking** 
		- [ ] [Martin et al. 2021](https://chemrxiv.org/engage/chemrxiv/article-details/60c756f8bb8c1a4fa63dc6e2](https://chemrxiv.org/engage/chemrxiv/article-details/60c756f8bb8c1a4fa63dc6e2) 
			*State of the Art Iterative Docking with Logistic Regression and Morgan Fingerprints*
		- [ ] [Adeshina et al. 2020](https://www.pnas.org/doi/full/10.1073/pnas.2000585117](https://www.pnas.org/doi/full/10.1073/pnas.2000585117) 
			*Machine learning classification can reduce false positives in structure-based virtual screening*
	- Books
		- [ ] *Thanks for the Feedback* by Douglas Stone & Sheila Heen 
	
3. Computing 
	 - [x] run toxo gondii proteome through decision tree (2)
	 - [x] graph decision tree results

4. **Meetings**
	- [x] *Aug 15 Tues*
		- co-expression for Toxo 
		- 10:15 am
		- 5740 MSII 
	- [ ] *Aug 16 Wed*
		- weekly one-on-one with Matt
		- 1:00 pm 
5. Calculus 
	Calc 2
	- [ ] Unit 6
	Calc 3 
	- [ ] Unit 1
	- [ ] Unit 2
	
## To do for next week
1. GRFP grant brainstorming
2. Readings not done this week 
3. Go to seminar
	- Date:  Thu 24 Aug
	- Time:  2pm-3pm (refreshments at 1:45pm)
	- Presenter:  Habib Hamidi, “Exploratory Analysis of High Dimensional Biomarker Data to Understand Molecular Heterogeneity and  Inform Novel Precision Medicine Based Clinical Trial Design”
	- THSL Room 2903 or Zoom 
4. *Automating Inequality: How High-Tech Tools Profile, Police, and Punish the Poor* by Virginia Eubanks
5. Calculus 
	- [ ] Unit 3
	- [ ] Unit 4
	- [ ] Unit 5

# Aug 16, 2023 (Wed)

## Questions
1. how to pay tuition? due on aug 30th amy
## Things discussed 
figure out which toxo reference proteome should be used for the structure predictions 
toxo db might be better than uniprot for finding the right reference proteome 
need to ask other colabs 

work on getting dock running 

data curation of tgcpl activities-- use to benchmark our models and will be used to generate the actives. we can create a ml model to classify the ligands into best and worst 

can make similar tables with docking results and docking models 
given a list of ccg numbers, get representations of the molecule

# Aug 23, 2023 (Wed)
