## Problem: ML models focus on one group in training and can't be applied well to a new data set 
- we only have access to training data (ann arbor hospitals) not test data (not detroit hospitals)
- model parameters are estimated via empirical loss minimization 
- baseline model f(x) is a pre-trained BERT model 
- not looking at MSE but instead the model performance is evaluated using worst-group accuracy to avoid hiding the worst performance (performance in predictions involving minority groups in training/test data)

## Solutions Currently
- minimax robustness 
	- take the max errors from all the parameters and then minimize those losses
	- train the model to minimize the error of the worst performing group 
	- assumptions: 
		- low worst-group error on training set 
			- low worst group error on out of distribution test set 
## Improved Solution 
- instead of focusing on one worst performing group, focus on multiple poorly performing groups in training data 
- helps mitigate the issue that one worst performing group may not be the worst group in the test data which can lead to poor out of distribution generalization 
- performing "smoothing"

## How to perform smoothing
- used information retrieval literature and use discounted cumulative gain (DCG- logarithmic criteria to weigh search results, for ex)
- DCG assigns decreasing weights to ranked items (high to low) 
- DCG will weigh worst performing groups in a logarithmic decrease way which decay fast initially but then slows down 

## Discounted rank up-weighting (DRU)
- algorithm to rank group performance via soft-minimax
- iterate over training data 
- rank all groups during epoch based on previous epoch 
- minimizes the loss function by using the weighting function produced from DRU and gradient descent 
- upweights all the samples in a group based on last epoch ranked group errors 
- also can augment DRU to only upweight the misclassified examples from a given group 

## Why does DRU works?
- the baseline models perform worse on minority groups due to spurious relations. 
- baseline models depend on spurious relationships between labels to achieve high accuracy on majority groups 
- they assume that spurious features are present in ALL groups to varying degrees 
- connections to causal inference
- DRU can be seen as inverse propensity scores (IPW) weighting using group prediction errors 
- out of distribution: group that is not in training data but in test data 


## Strengths of DRU
- strong empirical performance
- no a-priori knowledge of spurious features 
- has connections to IPW 