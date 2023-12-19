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
>>> oom_kill event in StepId
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


