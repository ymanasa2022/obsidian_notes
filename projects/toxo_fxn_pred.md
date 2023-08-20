There are two proteomes of Toxoplasma Gondii on [Uniprot](https://www.uniprot.org/proteomes?query=(organism_id:5811))
***Running both through Jake's Decision Tree to understand the quality of structures available so they can be used to predict functions of the genes in Toxoplasma Gondii*** 
## Reference Proteome (Main)
Entry: [UP000001529](https://www.uniprot.org/proteomes/UP000001529)
Organism: [Toxoplasma gondii ME49]()
Protein Count: 8,315 
`grep '>' /nfs/turbo/umms-petefred/ymanasa/proteomes/REF_toxo_ME49.fasta | wc -l`
## Reference Proteome1
Entry: [UP000002226](https://www.uniprot.org/proteomes/UP000002226)
Organism:[Toxoplasma gondii (ATCC 50861 / VEG)](https://www.uniprot.org/taxonomy/432359 "Toxoplasma gondii (strain ATCC 50861 / VEG) (ATCC 50861 / VEG), taxon ID 432359") (organism_id:432359)
Protein Count: 8,404
Rank: [Strain](https://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?lvl=0&amp;id=432359)

A reference proteome is the complete set of proteins produced by an organism. The reference proteome can best represent all the proteomes in its group in terms of the majority of the sequence space and information.
[Reference Proteomes](https://proteininformationresource.org/rps/#:~:text=Reference%20Proteomes%20(RPs) (RPs) (algorithmically determined), are proteomes that are selected from Representative Proteome Groups (RPGs) containing similar proteomes calculated based on co-membership in UniRef50 clusters. 

## Reference Proteome2
Entry: [UP000002437](https://www.uniprot.org/proteomes/UP000002437)
Organism: Toxoplasma gondii (RH) (organism_id:5811)
Protein Count: 466
Rank: [Species](https://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?lvl=0&amp;id=5811)

## Other Proteome
Entry: [UP000557509](https://www.uniprot.org/proteomes/UP000557509)
Organism: Toxoplasma gondii (RH-88) (organism_id:5811)
Protein Count: 8,260

## Running the Decision Tree
1. Navigate to `/nfs/turbo/umms-petefred/jaschwa/upec-fxn-pred-decide-only` on lighthouse
2. Start a screen session
3. Run command: `./run.sh <path/to/fasta_file>`
*WARNING*: the output intermediate_files/ directory and decidedone.tmp should not exist when trying to run. `mv intermediate_files intermediate_proteome_files/` before running script. You cannot run the pipeline from multiple invocations. Only one at a time.
4. The decision tree output text file is: `intermediate_files/decide/decisions.txt`

***started running toxo_rh88_8260.fasta in [1093262.pts-4.lh-login2]on aug 15 1:05pm***
> took about 2 hours to run all 8260 proteins

***started running REF_toxo_gondii_466.fasta in [2143219.pts-9.lh-login1]on aug 15 10:17pm***
>took about 30 minutes to run 466 

***started running REF_toxo_ATCC59861.fasta in [1203074.pts-1.lh-sigbio-login1] on aug 16 11:54pm***

***started running REF_toxo_ME49.fasta on aug 16 6:53pm***

all decisions can be found in `/nfs/turbo/umms-petefred/ymanasa/proteomes/decisions/`

## Plotting the decisions 
To plot a breakdown of the decision outputs:
1. Download `/nfs/turbo/umms-petefred/ymanasa/proteomes/graphs/plot_proteome_decisions.py`
2. Download the decision tree output text file 
3. Run `plot_proteome_decisions.py `after changing lines 8 and 42
##### *Reference Proteome Toxoplasma Gondii ME49 (8,315 proteins)*
![[dec_toxo_me49_8315.png]]
-using this proteome for further co-expression analysis 
-only 111 proteins have an experimental structure/homolog in PDB 
-1868 structures have homologs in AFDB that exactly match query 
-4882 proteins have poorly modeled structures/homologs in AFDB 
-1441 do not have homologs and modeled structures in AFDB 
##### Toxoplasma Gondii ATCC 50861 Strain (8,404 proteins)
![[dec_toxo_ATCC50861_8404.png]]

##### Toxoplasma Gondii RH88 Strain (8,260 proteins)

![[dec_toxo_rh88_8260.png]]
-There are only 111 proteins with pdb structures 
-Only 1857 structures modeled by AlphaFold2
-There are 15 proteins that have a close match to structures in AlphaFoldDB
-4844 proteins that have a structure modeled by AlphaFold2 but the predictions were of very low quality (plddt score of less than 70% accuracy)
-1433 have no modeled or experimental structures anywhere 

##### ReferenceProteome of Toxoplasma Gondii RH Strain (466 proteins)

![[dec_ toxo_rh_466.png]]
-288 have a bad AF structure, 64 dont have PDB or AF structure and need to be modeled
-107 have an exact match to an AFDB structure
-only 5 have a PDB structure
