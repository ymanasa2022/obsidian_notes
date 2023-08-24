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
	- [x] sign up for mentor mentee workshop 
	- [x] send itemized bill from apple
	- [x] add yourself to appropriate mailing lists
	- [x] share this github repo with Matt 
		- [x] need to change visibility of the repo. can't seem to figure that out yet.
	- [x] cancel apple macbook order
	- [x] get keys to building room
2. Readings
	- **TgCPL**
		- [x] [[pogorzelska_2018]] 
			[*Cysteine cathepsins as a prospective target for anticancer therapies—current progress and prospects*](https://pubmed.ncbi.nlm.nih.gov/29870804/)
		- [x] [Larson et al. 2009](larson_2009)
			[*Toxoplasma gondii Cathepsin L Is the Primary Target of the Invasion-inhibitory Compound Morpholinurea-leucyl-homophenyl-vinyl Sulfone Phenyl*](https://www.jbc.org/article/S0021-9258(20)38515-X/fulltext)
	- Books
		- [x] *Thanks for the Feedback* by Douglas Stone & Sheila Heen 
	
3. Computing 
	 - [x] run toxo gondii proteome through decision tree (2)
	 - [x] graph decision tree results

4. **Meetings**
	- [x] *Aug 15 Tues*
		- co-expression for Toxo 
		- 10:15 am
		- 5740 MSII 
	- [x] *Aug 16 Wed*
		- weekly one-on-one with Matt
		- 1:00 pm 
5. Calculus 
	Calc 2
	- [x] Unit 6
# Aug 16, 2023 (Wed)

## Things discussed 
- TgCPL
	- figure out which toxo reference proteome should be used for the structure predictions 
		- toxo db might be better than uniprot for finding the right reference proteome 
		- need to ask experimentalists which proteome in toxo db is right 
	- work on getting DOCK3.8 running 
	- data curation 
		- clean up and organize experimental data 
		- used to benchmark our docking models
		- we can create a ml model to classify the ligands into best and worst 
## To do for the week
1. Admin
	- [x] email amy about finance and insurance stuff
	- [x] get DOCK3.8 license 
	- [x] Training: Healthy Relationships 
2. Reading 
	- **TgCPL**
		- [x] [Bender et al. 2021](bender_2021)
			[*A practical guide to large-scale docking*](https://www.nature.com/articles/s41596-021-00597-z](https://www.nature.com/articles/s41596-021-00597-z)
		- [x] [London et al. 2014](london_2014)
			[*Covalent docking of large libraries for the discovery of chemical probes*](https://pubmed.ncbi.nlm.nih.gov/25344815/)
	- Books
		- [x] *Thanks for the feedback* 
3. Computation
	- [x] learn how to run DOCK3.8 (using bender_2021 protocol and Marissa's help)
		- [x] git clone DOCK into umms-maom turbo
		- [x] make instructions for docking 
	- [x] data curation of [TgCPL activities](https://docs.google.com/spreadsheets/d/1Lo0Nc6OFRyUe0arYsGTmi4eR1rFFTiq_GEcoAIC9rmE/edit?usp=sharing)
	- [x] Finish graphing ME49 decision tree results
		- [x] run ME49 through decision tree
	
4. Calc 3 
	- [x] Unit 1
	
1. Meetings
	- [x] Meet with Lydia 
	- Tues 22 Aug 
	- 10-11 am
	- [x] Bioinformatics Orientation
	- Tues 22 Aug
	- 3:30-4:30pm

# Aug 23, 2023 (Wed)
## Things discussed
1. I think we should make some kind of project outline for the TgCLP docking project, similar to the one you made for co-expression project -- started making [my own](toxo_data_curation)
2. the data curation we are doing is for making a ligand dataset for retrospective assessment for tgcpl docking?
3. are we docking multiple receptor poses to multiple ligands or just multiple ligands to one receptor pose? are we also docking multiple receptors (human and tgcpl proteins?) with multiple ligands?
4. Met with Lydia about previous projects. She was suggesting I write a short application note for the journal of bioinformatics for our structure/function pipeline once its fully working. Passed on other projects with documentation. She thought it was cool that we were using it for toxo and hence thinks writing a short paper on this would be nice for me 
5. GRFP Eligibility: 
	- Individuals with prior graduate enrollment who have: (i) completed more than one academic year in any graduate degree-granting program, (ii) earned a previous master's degree of any kind (including Bachelor's-Master's degree), or (iii) earned a professional degree must meet the following requirements: not enrolled in a graduate degree program at application deadline, two or more consecutive years past graduate degree enrollment or completion at the application deadline (https://www.nsf.gov/pubs/2023/nsf23605/nsf23605.pdf)
	- Have completed no more than one academic year (according to institution's academic calendar) while enrolled in a graduate degree program
	- length of the Personal, Relevant Background and Future Goals Statement is three (3) pages (PDF). The maximum length of the Graduate Research Plan Statement is two (2) pages (PDF)
6. GRFP idea: needs to be a project that I will continue working on
	- examples of GRFPs?
	- Specific Aim 1: Docking to TgCPL (or another protein) in different capacities 
	- Specific Aim 2: Using ML to dock instead of larger simulations for downstream/higher resolution docking steps
	- need to think about broader impact/usage: educational outreach about toxo/docking simulations, etc 
	- intellectual merit and broader impact sections 
7. Prelims:
	- thinking of doing it end of first year/in the summer 
	- can it be on any topic? even one that im working on or does it need to be a topic different from what im working on?
## To do for the week
1. Meetings
	- [ ] Weekly one-on-one with Matt 
	- Wed 23 Aug
	- 1-2pm
	- [ ] Bioinformatics Kickoff
	- Thus 24 aug
	- 1:30-8:30pm
2. GRFP grant brainstorming
	- [ ]  write outlines
3. Reading
	- TgCPL
		- [ ] R01 grant paper
		- [ ] Zwicker et al, 2018
			*Optimization of dipeptidic inhibitors of cathepsin L for improved Toxoplasma gondii selectivity and CNS permeability* 
		- [ ] Di Cristina et al, 2017
			*Toxoplasma depends on lysosomal consumption of autophagosomes for persistent infection*
	- ML Docking
		- [ ] [Martin et al. 2021](martin_2021) 
			[*State of the Art Iterative Docking with Logistic Regression and Morgan Fingerprints*](https://chemrxiv.org/engage/chemrxiv/article-details/60c756f8bb8c1a4fa63dc6e2)
		- [ ] Improving Screening Efficiency through Iterative Screening Using Docking and Conformal Prediction
		- [ ] [Adeshina et al. 2020](https://www.pnas.org/doi/10.1073/pnas.2000585117) 
			*Machine learning classification can reduce false positives in structure-based virtual screening*
		- [ ] Coleman et al, 2013
			*Ligand Pose and Orientational Sampling in Molecular Docking*
		- [ ] Dara et al, 2022
			*Machine Learning in Drug Discovery: A Review*
		- [ ] Graff et al, 2020
			*Accelerating High-Throughput Virtual Screening Through Molecular Pool-Based Active Learning*
		- [ ]  Gentile et al, 2020
			*Deep Docking: A Deep Learning Platform for Augmentation of Structure Based Drug Discovery*
4. Computation: 
	- [ ] set up new laptop
	- [ ] make git repo for docking 
	- [ ] make database for docking
	- [ ] start docking
5. Calculus 3
	- [ ] Unit 2
	- [ ] Unit 3
	- [ ] Unit 4
	- [ ] Unit 5