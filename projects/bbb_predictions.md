Predicting whether our current compounds with cross the blood brain barrier or not 
## Deciding which model to use
- looking at leaderboard: https://tdcommons.ai/benchmark/admet_group/07bbb/

| ***Rank*** |***Model*** | ***Trained on*** | 
| - | - | - | 
| 1 | [CFA](https://chemrxiv.org/engage/chemrxiv/article-details/6563ec17cf8b3c3cd73212b3) | 22 datasets in Therapeutics Data Commons |
| 2 | MapLight | | 
| 3 | Lantern RADR Ensemble | | 
| 4 | MapLight+GNN | | 
| 5 | Lantern RADR Deep Neural Network | | 
| 6 | ZairaChem | | 

## CFA
in conda environment: `docking`
https://chemrxiv.org/engage/chemrxiv/article-details/6563ec17cf8b3c3cd73212b3
- RDKit2D descriptors as input
https://github.com/F-LIDM/CFA4DD
https://pypi.org/project/cfanalysis/
- to change from SMILES to RdKit2D descriptors: 
	- https://www.blopig.com/blog/2022/06/how-to-turn-a-molecule-into-a-vector-of-physicochemical-descriptors-using-rdkit/
- generated molecular features: 
	- Morgan Circular Fingerprints 
	- RDKIT 2D descriptors
	- MCFP
- 5 algorithms used as a base model (feature and model fusion techniques)
	- XGB: implementation of Gradient Boosted Trees
	- RF: Random Forest
	- SVM: Support Vector Machine w linear kernel 
	- ADB: AdaBoost
	- CNN: Convolutional Neural Nets
- Dataset D.1 is what we are interested in using (BBB_Martins)
	- In table 4, for D.1, the best CFA combined model is BCE_ps: 0.920
	- BCE = RF, SVM, CNN. ps= weighted combination by performance strength 
- code for BBB_martins dataset is available in their gitrepo 
	- can be used to train 
	- prediction can be done for our ligands using CFA+RDKit.ipynb code?
## MapLight
- working locally (in Desktop/)
	- `git clone https://github.com/maplightrx/MapLight-TDC.git`
	- starting an env with mamba didn't work 
	- `conda create -y -n maplight python=3.10`
	- `conda activate maplight`
## Lantern RADAR
- https://github.com/lanternpharma/tdc-bbb-martins
- cloned repo into `/turbo/ymanasa/opt/`
- had issues with environment set up -> had to update conda i think 
- conda env: tdc created 
- having path issues with code in `/nfs/turbo/umms-maom/opt/tdc-bbb-martins/code/logistic.py`
- original:
	 `data_path = '/code/data/tdc_bbb_martins_ml_data/'`
	 `corr_feature_path = '/code/data/correlated_features/'`
- error:
	- `FileNotFoundError: [Errno 2] No such file or directory: '/code/data/tdc_bbb_martins_ml_data/trainval.tsv'`
	- fixed by setting: `data_path` and `corr_feature_path = 'data/tdc_bbb_martins_ml_data/'`
again same error in random_forest.py and the other python scripts in run.sh
fixed those and running again in interactive slurm sesh 
`srun -A maom0 -p standard --mem=1G -t 8:00:00 --pty /bin/sh`
>>> oom_kill event 
- running without srun 
	- linear regression works
	- random forest works
	- svm_linear works 
	- dnn works
	- ensemble works
## Baseline Training 
- Train the model using a dataset of interest
	- **BBB (Blood-Brain Barrier), [Martins et al](https://pubs.acs.org/doi/10.1021/ci300124c).** 2012
		- Scaffold splitting: https://www.oloren.ai/blog/scaff-split
		- 2053 molecules -> 1970 were used for modeling 
		- 1570 BBB+ and 483 BBB- molecules
		- `BBB_martins_2012.ipynb` has the dataset
	- [Nishant et al.]( https://ieeexplore.ieee.org/abstract/document/10182598?casa_token=IIEhoZpNWZ4AAAAA:qSbkqcyJeaxTPqAgO-XfRiwORDxiztPHCx0YZace4KFLzhzWet8P_iMkPZ5Zpi2TtyeOVCHR) 2023
		- 12764 compounds
		- cant find dataset
	- [Meng et al.](https://www.nature.com/articles/s41597-021-01069-5#Sec9) 2021
		-  50 distinct source including BBB Martins
		-  InChI is unique in principle, it cannot resolve tautomeric forms, which is a common source of ambiguity and error in chemical structure representation. Therefore, we examined the unique InChI generated with RdKit and the isomeric SMILES
		- has categorical (BBB- and BBB+ and BBB data with log BB values)
		- `logBB` values (1058 compounds), while the whole dataset has categorical (BBB+ or BBB-) BBB permeability labels (7807 compounds)
		- https://github.com/theochem/B3DB
		- I wrote a python script to find the common ligands from both and assigned unique identifiers to each compound 
### Meng et al 
- `/Users/ymanasa/Library/CloudStorage/OneDrive-MichiganMedicine/1PhD/omeara_lab/TgCPL/Data/BBB/B3DB_classification_uniq_ids.csv`
- `/Users/ymanasa/Library/CloudStorage/OneDrive-MichiganMedicine/1PhD/omeara_lab/TgCPL/Data/BBB/B3DB_unique_ligands.csv`
- `/Users/ymanasa/Library/CloudStorage/OneDrive-MichiganMedicine/1PhD/omeara_lab/TgCPL/Data/BBB/B3DB_regression_uniq_ids.csv`
## Make predictions 
- for Martin's ligands

# Similarity Searching
- need to show that the training set is a good representation of the molecules that we are predicting the BBB-/BBB+ for 
- can either use fingerprints or embeddings of the ligands to do similarity searches 
	- a pretrained model is used to create embeddings from the fingerprint parquet file
	- *embeddings* are normally used to representing a molecule in multidimensional space 
	- *molecular fingerprinting* is a type of *embedding*
- ECFP4: Extended-Connectivity Fingerprints with a diameter of 4 atoms
## Fingerprints for Training set
- Training set: Meng B3DB 2021
	- created a csv with the B3DB data along with unique ids for each molecule 
		- compound_names and uniq_ids have same values 
		- BBB-/BBB+ info included as well 
	- wrote python script to only keep unique molecules from regression and classification set: ![[remove_duplicates.ipynb]]
	- final csv made: B3DB_classification_sim_search.csv
- [Collab notebook](https://colab.research.google.com/drive/10-KbaJKF-ZjO9fyT_3wyELaKWqRWdiiS?usp=sharing) to create fingerprints/embeddings for all training set
	- using all compounds (from:` B3DB_classification_sim_search.csv`) 
	- input into collab notebook for fingerprinting: 
		- need: uniq_ids, SMILES, compound_name
		- fingerprint type: ECFP4
		- input: `B3DB_classification_sim_search.csv`
		- output: `fingerprints.parquet` file -> `B3DB_classified_ECFP4.parquet`
			`B3DB_ECFP4.parquet`: doesnt have BBB-/BBB+
	- input into collab notebook for PCA: 
		- need: uniq_ids, SMILES, compound_name
		- columns 2,3,5 of `B3DB_classification_uniq_ids.csv `
#### Clustering
- can visualize groups of the BBB- and BBB+ molecules in a lower dimension
- done using the Embed Molecules part in this [Collab notebook](https://colab.research.google.com/drive/10-KbaJKF-ZjO9fyT_3wyELaKWqRWdiiS?usp=sharing)
- embedding molecules into a lower dimensional space using PCA and UMAP (embed_umap command)
- --pca_n_components 200 ? 
	- says: `Reducing the dimension by PCA from 2000 to 200 dimensions`
	- BBB- is red
	- BBB+ is blue
![[umap_B3DB.png]]
## Fingerprints for TgCPL ligands
- input: `tgcpl_substances.smi` ->` tgcpl_ligs.csv `
	- need: uniq_ids, SMILES, compound_names 
	- using uniq_ids for compound_names
	- fingerprint type: ECFP4
	- input: `tgcpl_ligs.csv`
	- output: `fingerprints.parquet` file -> `tgcpl_ECFP4.parquet `
## Similarity search
- https://github.com/maomlab/MPLearn/blob/master/MPLearn/chemoinformatics/similarity_search.py
- MPLearn can be used to find tanimoto similarity 
	- computes the similarity of each ligand in our experimental set (Martin) to each compound in the training set (Meng)
- wrote `/home/ymanasa/turbo/opt/MPLearn/MPLearn/chemoinformatics/sdf_convert.py`
	- converts the library csv file into an sdf file that can be used by this script for similarity search`/home/ymanasa/turbo/opt/MPLearn/MPLearn/chemoinformatics/similarity_search.py`
	- sdf file: `/home/ymanasa/turbo/projects/TgCPL/BBB_preds/B3DB_classified.sdf`
- wrote `/home/ymanasa/turbo/opt/MPLearn/MPLearn/chemoinformatics/smi_similarity_search.py` to create input for similarity_search.py -> library_search() fxn
	- when threshold is 0.6: ![[tanimoto_bbb_0.6.png]]
	- should i worry about the ambiguous sterochemistry?-- Might be because i drew molecules using ChemDraw to get SMILES 
		- no hits when threshold is 0.5
	- when threshold is 0.4 (# of warnings are lower) there are hits: ![[tanimoto_BBB_0.4.png]]
	