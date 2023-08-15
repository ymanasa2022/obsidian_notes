There are two proteomes of Toxoplasma Gondii on [Uniprot](https://www.uniprot.org/proteomes?query=(organism_id:5811))
Running both through Jake's Decision Tree 

## Reference Proteome
Entry: [UP000002437](https://www.uniprot.org/proteomes/UP000002437)
Organism: Toxoplasma gondii (RH)
Protein Count: 466

A reference proteome is the complete set of proteins produced by an organism. The reference proteome can best represent all the proteomes in its group in terms of the majority of the sequence space and information.
[Reference Proteomes](https://proteininformationresource.org/rps/#:~:text=Reference%20Proteomes%20(RPs) (RPs) (algorithmically determined), are proteomes that are selected from Representative Proteome Groups (RPGs) containing similar proteomes calculated based on co-membership in UniRef50 clusters. 

## Other Proteome
Entry: [UP000557509](https://www.uniprot.org/proteomes/UP000557509)
Organism: Toxoplasma gondii (RH-88)
Protein Count: 8,260

## Running the Decision Tree
1. Navigate to `/nfs/turbo/umms-petefred/jaschwa/upec-fxn-pred-decide-only` on lighthouse
2. Start a screen session
3. Run command: `./run.sh <path/to/fasta_file>`
*WARNING*: the output intermediate_files/ directory and decidedone.tmp should not exist when trying to run. `mv intermediate_files intermediate_proteome_files/` before running script. You cannot run the pipeline from multiple invocations. Only one at a time.
4. The decision tree output text file is: intermediate_files/decide/decisions.txt

***started running toxo_rh88_8260.fasta in [1093262.pts-4.lh-login2]on aug 15 1:05pm***


