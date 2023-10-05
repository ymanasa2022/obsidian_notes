# Denoising Diffusion Probabilistic Models
https://proceedings.neurips.cc/paper/2020/file/4c5bcfec8584af0d967f1ab10179ca4b-Paper.pdf
- diffusion models are inspired by considerations from nonequilibrium thermodynamics
- best results: training on weighted variational bound designed 
- denoising score matching with Langevin Dynamics
- Inception score of 9.49 and FID score of 3.17 

## Intro
- diffusion probabilistic models: parameterized Markov Chain trained using variational inference 
- certain parameterization of diffusion models reveals an equivalence with denoising score matching over multiple noise levels during training and with annealed Langevin dynamics during sampling 
- their models do not have competitive log likelihoods compared to other likelihood-based models 
- sampling procedure of diffusion models is a type of progressive decoding that resembles autoregressive decoding along a bit 

# SE(3) diffusion model with application to protein backbone generation 
https://openreview.net/pdf?id=m8OUBymxwv
- backbones of proteins are represented as rigid frames (T element of SE(3)) which reduces degrees of freedom, has ideal intra-resiude bond lengths and angles but might have unphysical peptide bond geometry (similar to alpha fold modeling) 
- T is broken into SO(3) (Rotation) and R^3 (Translation). Can model diffusion on both independently 
- Priors: Uniform distribution of rotations in 3D space
## Figure 1: shows the method overview 
![[se3_diffusion_model.png]]
### A. 
- x: position of C alpha in 3D space
- r: ideal bond length. constructs the T matrix 
- T: Transformation. rotational and orientation matrix for the whole frame
- phi: torsion angle for backbone oxygen (we dont know where oxygen is placed)
The only degrees of freedoms are the (r,x) in T 

## Preliminaries and Notation 
- backbone parameterization was adopted from the backbone frame parameterization used in AF2 
- trying to denoise frames to get prior distribution 
- X(t): distribution of the data at time step t 
- dX(t): change of data distribution over time 

#### Denoising score matching 
- move in the direction to minimize the loss function 

## Results 
- how to evaluate the model: designability, diversity and novelty networks 
	- noise -> frame diff -> generated backbone -> use protein MPNN to generate a sequence of amino acids with generated backbone -> ESMFold to get predicted structure
	- they measure the accuracy of that structure and compare it to the backbone generated
	- rmsd: predicted structure match the generated structure 
	- how similar are the generated backbone structures to the pdb TM scores (backbones in pdb)