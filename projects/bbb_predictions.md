Predicting whether our current compounds with cross the blood brain barrier or not 
## Deciding which model to use
- looking at leaderboard: https://tdcommons.ai/benchmark/admet_group/07bbb/

| ***Rank*** |***Model*** | ***Trained on*** | 
| - | - | - | 
| 1 | [CFA](https://chemrxiv.org/engage/chemrxiv/article-details/6563ec17cf8b3c3cd73212b3) |  |
| 2 | MapLight | | 
| 3 | Lantern RADR Ensemble | | 
| 4 | MapLight+GNN | | 
| 5 | Lantern RADR Deep Neural Network | | 
| 6 | ZairaChem | | 

## CFA
https://chemrxiv.org/engage/chemrxiv/article-details/6563ec17cf8b3c3cd73212b3
- 
## MapLight
- working locally (in Desktop/)
	- `git clone https://github.com/maplightrx/MapLight-TDC.git`
	- starting an env with mamba didn't work 
	- `conda create -y -n maplight python=3.10`
	- `conda activate maplight`
## Baseline Training 
- Train the model using a dataset of interest
	- **BBB (Blood-Brain Barrier), Martins et al.** 
		- Scaffold splitting: https://www.oloren.ai/blog/scaff-split
## Make predictions 
- for Martin's CDD ligands
- the SAR Master's table ligands as well 