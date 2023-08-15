## Aug 15, 2023 (Tues)
### Using Co-Expression to Get Gene Function Predictions 
- what do genes do? answered using GO terms 
- if expression of a group of genes is correlated, the genes might be involved in the same process
- find the co-expressed partners of a gene and find what the partners are involved in to find out function of gene of interest
- can make co-expression networks (done with Theresa)
- creating a co-expression network for Toxo 
- normally done by bioinformatics people who don't have domain expertise are doing it in a superficial way. need to be more accessible to the community 
- Bulk RNA seq is the data not single cell 
	- NCBI seq read archive (https://www.ncbi.nlm.nih.gov/sra) raw data
	- NCBI geo (https://www.ncbi.nlm.nih.gov/geo/) cleaned up data and expression value for each gene 
		- baseline for all data is different based on different people so using raw data is better
	- which studies and which samples we use will give us a filtered list 
	- manually assessment of all the studies are needed 
	- may not have an assessment score with the reads in the database 
- Differential expressional analysis
	- various different experimental perturbations 
	- gene expression studied for each perturbation in multiple samples
	- bulk rna seq done for each sample 

#### Decision Tree 
[Run proteome through decision tree to understand structure availability of proteins in Toxo Proteome](toxo_fxn_pred.md) 

