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
1. I think we should make some kind of project outline for the TgCLP docking project, similar to the one you made for co-expression project -- started making [my own](toxo_dock_outline.md)
2. the data curation we are doing is for making a ligand dataset for retrospective assessment for tgcpl docking? yes
3. are we docking multiple receptor poses to multiple ligands or just multiple ligands to one receptor pose? are we also docking multiple receptors (human and tgcpl proteins?) with multiple ligands?
4. Met with Lydia about previous projects. She was suggesting I write a short application note for the journal of bioinformatics for our structure/function pipeline once its fully working. Passed on other projects with documentation. She thought it was cool that we were using it for toxo and hence thinks writing a short paper on this would be nice for me 
5. GRFP Eligibility: Not eligible
	- Individuals with prior graduate enrollment who have: (i) completed more than one academic year in any graduate degree-granting program, (ii) earned a previous master's degree of any kind (including Bachelor's-Master's degree), or (iii) earned a professional degree must meet the following requirements: not enrolled in a graduate degree program at application deadline, two or more consecutive years past graduate degree enrollment or completion at the application deadline (https://www.nsf.gov/pubs/2023/nsf23605/nsf23605.pdf)
	- Have completed no more than one academic year (according to institution's academic calendar) while enrolled in a graduate degree program
	- length of the Personal, Relevant Background and Future Goals Statement is three (3) pages (PDF). The maximum length of the Graduate Research Plan Statement is two (2) pages (PDF)
6. GRFP idea: needs to be a project that I will continue working on
	- examples of GRFPs?
	- Specific Aim 1: Docking to TgCPL (or another protein) in different capacities 
	- Specific Aim 2: Using ML to dock instead of larger simulations for downstream/higher resolution docking steps
	- need to think about broader impact/usage: educational outreach about toxo/docking simulations, etc 
	- intellectual merit and broader impact sections 
1. Prelims:
	- can only do it after finishing core requirements 
	- can it be on any topic? even one that im working on or does it need to be a topic different from what im working on?
## To do for the week
1. Meetings
	- [x] Weekly one-on-one with Matt 
	- Wed 23 Aug
	- 1-2pm
	- [x] Bioinformatics Kickoff
	- Thus 24 aug
	- 1:30-8:30pm
2. ~~GRFP grant brainstorming?~~
	- [x]  write outlines
***Im not eligible for GRFP*** 
1. Reading
	- TgCPL
		- [ ] R01 grant paper
		- [ ] Zwicker et al, 2018
			*Optimization of dipeptidic inhibitors of cathepsin L for improved Toxoplasma gondii selectivity and CNS permeability* 
		- [ ] Di Cristina et al, 2017
			*Toxoplasma depends on lysosomal consumption of autophagosomes for persistent infection*
	- ML Docking
		- [ ] [Martin et al. 2021](martin_2021) 
			[*State of the Art Iterative Docking with Logistic Regression and Morgan Fingerprints*](https://chemrxiv.org/engage/chemrxiv/article-details/60c756f8bb8c1a4fa63dc6e2)
			what is enrichment???
		- [ ] Improving Screening Efficiency through Iterative Screening Using Docking and Conformal Prediction
		- [ ] [Adeshina et al. 2020](https://www.pnas.org/doi/10.1073/pnas.2000585117) 
			*Machine learning classification can reduce false positives in structure-based virtual screening*
		- [ ] Coleman et al, 2013
			*Ligand Pose and Orientational Sampling in Molecular Docking*
		- [ ] Graff et al, 2020
			*Accelerating High-Throughput Virtual Screening Through Molecular Pool-Based Active Learning*
		- [ ]  Gentile et al, 2020
			*Deep Docking: A Deep Learning Platform for Augmentation of Structure Based Drug Discovery*
4. Computation: 
	- [x] set up new laptop
	- [x] make git repo for docking 
	- [ ] make database for covalent docking
	- [ ] start docking
# Aug 30, 2023 (Wed)
## Things Discussed 
- make [library](toxo_dock_outline.md) using guide to pharmacology.com, chemb, pubchem, binding db
	- one zinc id might correspond to different chmbl molecules. toxoplasma cpl and human cpL
	- get list of compounds from pChEMBL for a given target
	- for a given assay, get list of compounds 
	- take out ones with low pChEMBL Values and ones with comments in data validity. repeat for human cpl
- Test running [Covalent](covalent_docking_test.md) docking on greatlakes with existing database 
## To do for the week
- [x] curate small compounds that dock to tgcpl
	- R05 Violations (drug bioaccessibility rules)? if more than 0, take out?
	- some dont have pchembl values
	- took out "not active" compounds from comment column 
	- molecular weight limit?
	- took out all "outside typical range" from data validity column
	- couple of rows at the end of the file have blank columns in HsCPL_ligand_activities
- [x] test and debug covalent docking 
- [x] explore fellowship requirements https://www.hertzfoundation.org/the-fellowship/
	- not sure where to get four recommenders
- [x] read BIOINF 602 paper 
	- [x] **[Human population-specific gene expression and transcriptional network modification with polymorphic transposable elements](https://academic.oup.com/nar/article/45/5/2318/2725373)**
- [x] read BIOSTATS textbooks
	- [x] watch videos on counting etc
	- [x] finish HW 
	- [x] decide whether to switch to STATS 425 (wont be swithcing)
- [ ] finish reading:
	- [ ]  [Martin et al. 2021](martin_2021) 
			[*State of the Art Iterative Docking with Logistic Regression and Morgan Fingerprints*](https://chemrxiv.org/engage/chemrxiv/article-details/60c756f8bb8c1a4fa63dc6e2)
	 - [ ] [Adeshina et al. 2020](https://www.pnas.org/doi/10.1073/pnas.2000585117) 
			*Machine learning classification can reduce false positives in structure-based virtual screening* 
# Sep 6, 2023
## Things Discussed 
- data curation for HsCPL and TgCPL 
	- remove anything that doesnt report in nM (needs to be less than 1000nM for IC50 and Ki)
	- Inhibition given in percentages need to be taken out 
	- take out all "not active" compounds and "outside typical range"
	- take out anything with empty columns 
	- IC50 is very similar to Ki (K inhibition constant). Ki is slightly more accurate than IC50.
		- IC50 is how much drug is needed to inhibit the protein function by 50% 
		- Ki is an indicator of how potent an inhibitor is
- test covalent docking with datasets in `/home/ymanasa/turbo/CovalentLibs/unsubstituted-acrylamides `and `/home/ymanasa/turbo/CovalentLibs/beta-sub-acrylate-esters`
	- previous covalent docking methods used zinc instock database which have ligands that arent made for covalent docking
		- covalent docking involved adding a Si atom to the ligand structure pointing the program to dock this Si atom to the specified residue on the protein target 
		- the zinc instock ligands did not have these Si atoms and therefore covalent docking was not possible to do with tgcpl 
- hit screening using chimera 
	- maybe try to automate
	- need three files (examples can be found in: `/Users/ymanasa/Library/CloudStorage/OneDrive-MichiganMedicine/omeara_lab/TgCPL/Docking/example_hit_screen`)
		1. load rec.crg.pdb and xtal-lig.pdb 
		2. do visual manipulations to make one pdb transparent and the other not 
		3. make sure you can visualize the original drug ligand in the protein pocket
		4. load the poses.mol2 file that come from after processing the docking results on greatlakes 
		5. use visual analysis to decide which ligands to keep and which ones to discard 
- work on the grant 
	- email Dr. Uhler-- probably meet up with him 
	- email Dr. Paula-- zoom?
## To do for the week 
- [x] finish data curation for HsCPL and TgCPL
- [x] test covalent docking with unsubstituted-acrylamides 
- [x] test covalent docking with beta-sub-acrylate-esters
- [x] email Dr. Paula 
	- [ ] set up zoom time (she wont respond until sept 15)
- [x] email Dr. Uhler and Dr. Thompson
	- [ ] set up meetup time 
- [x] start looking into grant application 
	- Essays needed (~300 words each):
		- Question 1 Essay - How did you choose your field and what are your primary expectations of your future career?
		- Question 2 Essay - How does your proposed field of study and career constitute an application of the physical sciences or engineering?
		- Question 3 Essay - What are the considerations involved in your choice of graduate school?
		- Question 4 Essay - Chronological Synopsis
		- This is an opportunity for you to share your narrative with experiences that demonstrate your creativity, perseverance, curiosity and/or grit. Personal Essay response
		- Academic Honors: dean's list
		- list research projects and choose one or two projects that best exemplify your own creativity and discuss in more detail what you personally contributed to them.x`
- [ ] finish practice problems for BIOSTAT 602 HW1
- [x] read BIOINF 602 paper 
	- [x] [Viral genomes reveal patterns of the SARS-CoV-2 outbreak in Washington State](https://www.science.org/doi/full/10.1126/scitranslmed.abf0202?rfr_dat=cr_pub++0pubmed&url_ver=Z39.88-2003&rfr_id=ori%3Arid%3Acrossref.org)
- [ ] finish BIOSTAT 601 HW 
- [x] finish BIOINF 500 HW 
- [x] finish BIOINF 575 exercises
- [x] finish reading:
	- [x]  [Martin et al. 2021](martin_2021) 
			[*State of the Art Iterative Docking with Logistic Regression and Morgan Fingerprints*](https://chemrxiv.org/engage/chemrxiv/article-details/60c756f8bb8c1a4fa63dc6e2)
- [x] watch: [https://www.youtube.com/@SerranoAcademy](https://www.youtube.com/@SerranoAcademy) 
- [x] Finish training: Cultivating a Culture of Respect

# Sep 13, 2023
## Things Discussed 
- data curation for commercially available ligands used in covalent docking 
	- Take out ED50s if done in animal models and if greater than 1uM standard value 
	- if done in cells dont remove. functional assays too rather than molecular assays 
- CDD vault for testing retrospective docking using experimentally assessed ligands 
	- why are some missing in the search (126 out of 133 showing)
	- need to figure out how to pull molecules and pull activity data 
	- look at tutorials or manuals 
- covalent docking with unsubstituted-acrylamides 
	- androgen_20230818,zinc_instock,,20230908 (works)
	- androgen_cov_20230908,zinc_instock,,20230908 (works)
	- tgcpl_cov_20230911,unsubstituted_acrylamides,,20230911
	- tgcpl_cov_20230911,zinc_instock,tgcpl_zinc,20230911
	- androgen_cov_20230908,unsubstituted_acrylamides,,20230911
	- tgcpl_cov_20230911,unsubstituted_acrylamides_lead-like,,20230911
	- tgcpl_cov_20230911,beta_sub_acrylate_esters_frag,,20230911
	- fragments or lead-like? just do both but start with fragments. they are better (bc they are smaller, easier to synthesize, less metabolic liabilities) 
	- add lines from: `${DOCK_TEMPLATE}/scripts/dock_indock_tight_covalent.sh` `2_finalize_structure.sh`to `/home/ymanasa/opt/dock_campaign_template/prepared_structures/TEMPLATE_COVALENT/2_finalize_structure.sh` (then commit)
- covalent docking with beta-sub-acrylate-esters 
	- fragments or lead-like? start with fragments and then see how the hits look before doing lead-like docking
	- same issue as previous
- [ENAMINE](https://enamine.net/compound-collections/covalent-compounds)
	- commercial list of covalent compounds
	- might compare to these later 
	- preprints/reach out to DOCK: best covalent libraries to use with DOCK? 
		- Nir London, Widesman in Israel covalent dock 
- covalent interactions towards cys or lys. check geometries for hit poses
	- allow it to export clashes and see if we can change step size/covalent library/minimization to try to fit more properly to protein 
	- this is the docking model optimization step 
## Things to do 

- [x] fix covalent docking scripts 

- [x] read BIOINF 602 paper 
	- [x] [Spatial epigenome-transcriptome co-profiling of mammamlian tissues](https://www.nature.com/articles/s41586-023-05795-1)

- [x] do BIOSTAT 601 HW 
- [x] do BIOINF 575 HW
- [x] do BIOSTAT 601 Practice Qs

- [x] send emails to Uhler
- [x] send email to Paula

- [x] Tools & Tech Seminar (Thurs)
- [x] Diffusion MIDAS symposium (Fri)

# Sep 20, 2023
## Things Discussed
- debugging docking 
- matt concluded that DOCK 3.8 is the issue
	- need to use to DOCK 3.7 instead 
	- test database here: `/home/ymanasa/turbo/nSMase2/fragment_screen/databases/manasa1_test`
	- structure used: `/home/ymanasa/turbo/nSMase2/fragment_screen/prepared_structures/A0773_covalent_20220203`
	- docking run: `/home/ymanasa/turbo/nSMase2/fragment_screen/docking_runs/manasa_test1`
## Things to do 
- [ ] finish docking to unsub-acrylamides 
	- start with fragments

- [x] grant meetings?
	- [x] finalize meeting with uhler and thompson
	- [x] finalize meeting with paola

- [x] Tools and Tech (Thur)
- [x] BISTRO (Thur) 
- [x] Bioinf Retreat (Fri-Sat)

- [x] BIOSTAT 601 HW
- [x] BIOINF 575 HW 
- [x] BIOINF 575 HW

- [x] wed: 11am JC Rosetta Diffusion Models 
- [x] wed: 11:30am BIOSTAT Office Hrs 
- [x] wed: 1pm weekly one on one
# Sep 27, 2023
## Things discussed
- debugging docking 
	- docking with toxo and unsub acrylamides works 
	- continue with results and hit screening analysis
- prelim meeting
	- not bad idea to do prelim beginning of 2nd year
	- need to keep reading ml papers
	- https://www.bakerlab.org/2023/07/11/diffusion-model-for-protein-design/
	- RFDiffusion 
- CDD Vault
	- need to curate these once Martin is done uploading stuff 
	- SMILES and SMARTS needed to make covalent libraries 
- add to rosetta slack-- didnt get last message/email with paper details
## Things to do for the next week 
- [x] make dock3.7 work 
- [x] attempt docking to unsub-acrylamides 
	- start with fragments
- [ ] analyze results

- [ ] BIOSTAT 601 practice Qs
	- [ ] study for midterm (practice exam)
- [x] BIOINF 575 HW
- [ ] BIOINF 602 Reading 
- [x] BIOINF 500 HW 

- [x] attend update meetings 
	- [x] fri: 3pm Uhler + Thompson
	- [x] thur: 7:45pm Paola 
- [x] thur: tools and tech seminar 

- [x] benefits review 
# Oct 4, 2023
## Things discussed
- ***DOCK3.7 docking testing:*** 
	- made my own `1_run.sh` script called `1_submit.sh script `
	- changes were made to `/home/ymanasa/turbo/opt/DOCK37/analysis/extract_all_blazing_fast.py`
	- Take a look at `results/1/OUTDOCK.0`: 
		- doesn't seem complete
		- there's 5 ligands in 1.db2.gz and 10 poses for each were tested out 
		- awk '{print $1}' OUTDOCK.0  | grep '5' -> only 3 
		- the rest were 10 poses each
	- need to figure out why slurm job is ending early (might be a wall time issue: try adding $SLURMARG for wall time in 1_submit.sh for docking_run)
- ***docking analysis:***
	- changing python 2 code to python 3 in `/home/ymanasa/turbo/opt/DOCK37/analysis/extract_all_blazing_fast.py`
	- had to manually remove lines that didnt have valid energy entries (non int values)
	- getting this error when running **getposes_blazing_faster_py3.py**: 
	  `gzip: results/4/test.mol2.gz.0: unexpected end of file` -> might be because of the slurm issue
- ***poses analysis*** 
	1. File -> Open -> rec.pdb and poses.mol2
	2. Favorites -> Model Panel 
		- to show or hide molecules loaded
	3. Select -> Chain -> A -> rec.pdb 
		- to select receptor chain 
	4. Actions -> Atoms & Bonds -> show 
	5. Select -> chain -> A -> rec.pdb
	6. Actions -> Ribbons -> hide
	7. Select -> chain -> A -> rec.pdb
	8. Actions -> Surface -> show -> set transparency 70%
	9. Remove HC atoms from ligand 
	10. Tools -> Structure Analysis -> FindH bonds
	11. Tools -> Viewing -> Side View 
		- Surface capping: uncheck cap surfaces at clip panes 
		- change boundaries to focus on ligand in pocket
	12. Tools -> Surface Binding Analysis -> ViewDock -> Select all poses -> move to deleted 
	13. Assess if each ligand is forming reasonably accurate covalent bonds 
- ***dock other covalent subsets*** 
	- ENAMINE covalent libraries
- ***preparing project covalent ligands***:
	- must add *Si* atom to ligands at docking points
	- to get output.ism: `/home/ymanasa/turbo/CovalentLibs/scripts/unsat-ab-carbonyl.py `
	- input example in `/home/ymanasa/turbo/CovalentLibs/unsubstituted-acrylamides/fragments/smiles/unsub.frag.acrylamides.ism`
	- SMILES from Martin's excel 
	- SMILES vs SMARTS? 
	- get chemdraw to work 
	- use chem draw to assess reactions 
- ***R01 Update***
	- essentially want a 3D image and 2D image of the best ligand (from grant maybe or ENAMINE) in TgCPL 
	- proteins dock plus: pdb file input and finds the ligands to make 2D interaction figure 
## Things to do for the next week
#### HW 
- [ ] Skim BIOINF 602 paper for 10/11
- [ ] Really Read BIOINF 602 paper for Review 10/13
- [ ] BIOINF 575 HW
- [ ] BIOINF 601 HW
- [ ] PIBS 503 reading (10/5)
- [ ] PIBS 503 reading (10/6)
- [ ] Read Rosetta JC paper (RFDiffusion)

#### Research
