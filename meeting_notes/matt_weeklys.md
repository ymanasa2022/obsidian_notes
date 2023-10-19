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
- [x] analyze results

- [x] BIOSTAT 601 practice Qs
	- [x] study for midterm (practice exam)
- [x] BIOINF 575 HW
- [x] BIOINF 602 Reading 
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
	3. Select -> Chain -> A -> rec.pdb 
		- to select receptor chain 
	4. Actions -> Atoms & Bonds -> show 
	5. Select -> chain -> A 
	6. Actions -> Ribbons -> hide
	7. Select -> chain -> A 
	8. Actions -> Surface -> show -> set transparency 70%
	9. Actions -> Color -> by heteroatom (everything not C or H)
	10. Select -> Chemistry -> IDATM type -> HC 
	11. Actions -> Atom & Bonds -> hide
	12. Tools -> Structure Analysis -> FindH bonds
		- uncheck intra molecule and residue H bonds 
	13. Tools -> Viewing -> Side View 
		- Surface capping: uncheck cap surfaces at clip panes 
		- change boundaries to focus on ligand in pocket
	14. Tools -> Surface Binding Analysis -> ViewDock -> Select all poses -> move to delete
	15. in ViewDock -> Column -> Total Energy 
		- arrange based on total energy (more negative the better)
	16. Favorites -> Model Panel 
		- hide the first poses.mol2 
	17. Assess if each ligand is forming reasonably accurate covalent bonds 
		- change compound state to viable if ligand looks ok 
		- keep in deleted if not good
- ***dock other covalent subsets*** 
	- ENAMINE covalent libraries
- ***preparing project covalent ligands***:
	- must add *Si* atom to ligands at docking points
	- to get ligands prepped for covalent docking use: `/home/ymanasa/turbo/CovalentLibs/scripts/unsat-ab-carbonyl.py `
		- input file example in `/home/ymanasa/turbo/CovalentLibs/unsubstituted-acrylamides/fragments/smiles/unsub.frag.acrylamides.ism`
		- SMILES from Martin's excel 
	- SMILES vs SMARTS? 
	- get chemdraw to work 
	- use chem draw to assess reactions 
- ***R01 Update***
	- essentially want a 3D image and 2D image of the best ligand (from grant maybe or ENAMINE) in TgCPL 
	- proteins dock plus: pdb file input and finds the ligands to make 2D interaction figure 
## Things to do for the next week
#### HW 
- [x] Take BIOSTAT 602 Exam 
- [x] Skim BIOINF 602 paper for 10/11 https://www.nature.com/articles/s41587-021-00949-w
- [x] BIOINF 575 HW
- [x] PIBS 503 reading (10/5)
- [x] PIBS 503 reading (10/6)
- [x] Read Rosetta JC paper 

#### Research
- [x] change dock_template scripts 
- [x] move everything to turbo/projects/TgCPL dir
- [x] poses analysis
- [x] determine docking slurm issue 
	- [x] make sure it works
- [x] dock other covalent libraries 
- [ ] prepare covalent ligands from Martin 
	- [x] sent email to chem draw people for activation 
#### Meetings
- [x] attend PIBS 503 Mentoring Relationships Meeting
- [x] attend PIBS 503 Authorship & Peer Review (F)
- [x] Molecular Modeling Meeting (F)
- [x] ML JC Rosetta (10/11 W)
- [x] Weekly w. Matt (10/11 W)

# Oct 9, 2023
## Things discussed
- pose analysis
	- understand what the charges on each group are
		- we want non polar groups buried in the pocket 
		- lesser repulsive groups (oxygen in ligand and oxygen in receptor shouldnt be next to each other)
		- the Si atom placement dictates to the model where the covalent interaction will be taking place 
		- benzene rings sp2 hybridized -> negative?
	- understand the protonation states for functional groups in an acidic environment
		- our tgcpl is in lysome so the environment is slightly acidic not neutral (pH ~6.0-- confirm with literature)
		- pka calculations might be needed to confirm these protonation states 
			- either done by hand or use software (ask Matt)
	- need to do for all ENAMINE libraries
- pull request assessment ([[covalent_TgCPL_ENAMINE_libs]]) 
	- resolve git issues for docking_campaings repo 
	- slurm issues resolved 
- preparing ligands for covalent docking 
	- created `martin_cdd_09132023.ism` in `/home/ymanasa/turbo/CovalentLibs/martin_cdd`
	- used columns C D to create tab spaced file `martin_cdd_09132023.ism` 
	- need to use chem draw to figure out line 19 in `/home/ymanasa/turbo/CovalentLibs/scripts/martin_09132023.py`
	- how to know what the reactive group is?
		- compared to an unsat acrylamide example in smarts.plus using smirks reaction in python script and the first smiles in `/home/ymanasa/turbo/CovalentLibs/unsubstituted-acrylamides/fragments/smiles/unsub.frag.acrylamides.ism`
		- looking at the grant, we can tell that the ligands from Martin have nitrile warheads and hence we can use the heterocyclic nitrile warhead scripts to add Silicon atoms for covalent interactions
			- make sure they all have nitrile warheads on cdd
		- can use smarts.plus to view reaction strings from scripts 
	- make db2 files using tldr 
- prep human target 
- 
	- filter to a subset that will be good, have one or two backups-- have three; check if all are identical or if they have propeptides/open or close/ high res vs low res
	- check grant and relevant papers for HsCPL target structure
## Things to do for the next week
#### Research
- [x] keep docking ENAMINE libraries
	- need python scripts to add Si to work 
	- matt needs to respond with licensing info 
- [x] do pose analysis for docked enamine libraries 
- prepare Martin's ligands for covalent docking 
	- [x] comb cdd to make sure all are nitrile warheads of the same kind
- prepare db2 files for Martin's ligands 
	- need to prep with Si first
- [x] select human target
#### HW
- [x] BIOINF 500 HW (Sun 10/14)
- [x]  Really Read BIOINF 602 paper for Review  https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005595 (Fri 10/13)
- [x] BIOINF 575 (Th 10/19)

#### Meetings
- [x] BIOINF 602 Review Session (10/13 F)
- [x] Tools & Tech Seminar (10/12 T)
- [ ] BISTRO (10/18 Th)
- [x] Weekly Meeting with Matt (10/18 W)
- [x] BIOINF 575 Project Meeting (T 10/17)
# Oct 18, 2023

## Things discussed
- pose analysis
	- take top 0.1%? as suggested in [[bender_2021]]
		- clustering similar types of molecules and checking for the best one in each cluster 
		- could come up with filtering rules to get rid of molecules of the same type 
	- fastest way to get that:
		- bash: sort the extract_all.txt last total energy column and then compute top 0.1%?
- tldr vs OpenBabble (easier to just use tldr after using OpenEye) 
	1. add silicon atoms
	2. confirmation enumeration: ZINC uses OpenEye or RDKit 
	3. charge distribution in a compound, desolvation energies using programs (in bender)
- OpenEye Lisence
	- can use RDkit instead for SMIRKS patterns 
- other ENAMINE libraries (commericially avaialbel compounds): 
	- can ask around if other labs already have prepped the other libraries 
	- ENAMINE libraries on turbo might be too old (just use these for now)
	- might use covalent libraries being used currently (in google scholar papers)
- other libraries (warhead compounds) 
	- can get a much larger library 
	- ZINC: chemical search using warhead to get all the compounds of that type using the SMARTS pattern 
	- https://sw.docking.org/search.html
- HsCPL prep
	- aligned 4 
		- got structures from the curated list on TgCPL activity google sheet
		- also wanted 1CJL bc it was the structure used in the activity assays from ChemBL 
	- best resolution structure doesnt look right 
		- was thinking of using this for docking once i figure out which residue ligands are docked to
		- check what residues around the active site are different between toxo and human CPL 
	- select the ligand -> show residues within 8 A 
	- find the residues using protease pocket naming conventions (like P1,P2, etc) and find the residues that interact within the HsCPL pocket and TgCPL pocket 
	- identify the residues that are interacting with key residues in TgCPL and HgCPL 
		- can quantify to find if selective later 
	- DOCK is not great at confirmation sampling of the receptor 
		- can use Rosetta Docking to do different confirmations for the HsCPL 
	- check if the water molecules same in every structure 
		- using polar measurement 
	- use measure wizard tool to measure angles and bonds 
		- check covalent ligand angle bonds between all human cpl structures and the toxo hits 
		- Different trials: could dock to all four human targets (to asses natural variation of DOCK between same targets-- to see the consistency of ligand ranking)
	- can save scenes 
		- scene -> append -> right click lower left corner to rename scene and save
		- if you save session and reopen, the scenes will be saved with that session 
#### HW
- [ ] BIOSTAT 601 (10/19 Th)
- [ ] BIOINF575: Start Github Repo + Attempt Project (??)
- [ ] BIOINF 575 set up meeting time
- [ ] BIOINF 575 (10/25 Th)
- [ ] BIOSTAT 601 (10/25 Th)
- [ ] BIOINF 602 Reading (10/24 W)
- [ ] ML Rosetta JC (10/24 W)
#### Research
- [ ] prepare Martin's ligands for covalent docking 
- [ ] prepare db2 files for Martin's ligands 
- [ ] prep human target 
- [ ] docking to 4 human cathepsins
- [ ] continue pose analysis
- [ ] might want to make slides with key milestones/steps
#### Meetings 
- [ ] Tools & Tech (10/19 Th) 
- [ ] BISTRO (10/19 Th)
- [ ] Weekly Meeting with Matt (10/25 W)
- [ ] BISTRO (10/26 Th)
- [ ] BISTRO Activity (10/26 Th)

