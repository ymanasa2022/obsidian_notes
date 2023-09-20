## A tutorial on score-based generative models with medical imaging applications
### Intro 
- low dose sparse view x ray image generation 
- model from some probability distribution p(x)
- generative models: usually a method for drawing samples from that distribution 
- models depend on parameters (they work with a parametric model)
- challenge1: learning the parameters from some training data 
- challenge2: how to pick from that data/sample from a distribution of data 
- Maximum likelihood (ML) estimation to fit the two gamma distribution parameters requires an iterative model. still hard to draw samples 
- generating samples involve conditional distributions (p_teta(x|y))
##### Bayesian inference 
- given test data y related to a latent variable x
- known likelihood function p(y|x)
- want to estimate x from y 
- max likelihood estimation is insufficient for under determined problems 
- the prior info is the training data 
- maximizing p(x|y) is maximum a posteriori (MAP) estimation 
	- dont really need prior to sample from the prior 
	- just needs a scoring function using Langevin dynamics aka stochastic gradient descent (points towards more probable outcome) of log-prior 
- typical distribution models using a scoring function that has an energy function and a partition function 
	- learning Bayesian functions from training data is made hard by the partition function 
- you can recover the pdf from its scoring function (derivative of pdf) using anti derivative 
	- score function: takes in the number of parameters you are trying to model and the output is the same number of parameters
##### Learning a scoring function
- given training data, learn score function by p(x) is unknown 
		- nonparametric density estimation approach?
			- impractical test time 
			- kernel density estimate
		- parametric 
			- explicit score matching (ESM) 
				- estimate data distribution (kernel density estimation)
				- match model score to data score 
			- implicit score matching (ISM)
		- denoising score matching (DSM)
			- equivalence between ESM and DSM 
			- take your data, add noise and then get your model to reduce that noise to learn the scoring function 
			- need to use many different noise levels (distribution of noises- Noise-Conditional Score Matching (NSM))
			- if you know the scoring function you can recover the original data without the added noise 
- accelerating the sample generation process with enough training data. expensive sample generation methods: 
	- distillation methods
	- consistency models
	- geometric decomposition 
	- latent diffusion models 
- [Geman & Geman](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=4767596) 1984 Markov random field models 
	- MRF formulation: write our prior as a product of terms 
- could [patch-based](https://www.ecva.net/papers/eccv_2022/papers_ECCV/papers/136770547.pdf) generative models provide between robustness to distribution shifts, perhaps at the cost of reduced in-distribution performance?

## Diffusion Models for Inverse Problems in Medical Imaging
- Self supervised Denoising: SURE 
- Tweedie's formula for exponential family distribution 
	- using Baye's rule, obtain the posterior distribution
	- as long as we can compute the scoring function, optimal denoising can be achieved by using Tweedie's formula 
	- estimating x^ 
- relation to existing methods
	- p(x): training data 
	- score function: gradient of the log p(x). points towards the peak point of the density
	- denoising autoencover (DAE) close to Noise2X
		- can be used to estimate the score function of data y 
		- self supervised learning 
		- score based approaches 
- Noise2Score vs Diffusion Models
	- once score model is trained method1, 
		- use Langevin Dynamics (SMLD) to draw samples
	- or method2
		- Diffusion Denoising Probabilistic Model (DDPM) 
			- variance preserving parameterization 
- how to use for inverse problems?
	- have an unknown image x that you want to estimate from a y image (noised/lower quality image) without knowledge of prior data 
- score based diffusion models for accelerated MRI (Jung at al, MEDIA, 2022)
- To accelerate sample generation: Denoising Markov-Chain Monte Carlo (DMCMC)
- come closer diffuse faster (CCDF)
- 3D diffusion needs many many samples for training
	- decompose into the different planes x, y,z 
	- can generate the 3D model from three plane diffusion image generation 
## Plug and play methods for inverse problems: self-calibration, conditional generation and continuous representation 
- reverse problem: generate x from measurement y 
- y = A(x)  + e 
- MRI
	- data is collected in frequency space 
	- inverse Fourier transform to get the reconstructed image
	- longer data collection improves image quality but leads to increase patient discomfort 
- limited angle computer tomography 
	- collecting projections of the image (at different angles) to reconstruct the image
	- need a lot of angles but can use diffusion models to fill in missing data 
- intensity diffraction tomography (IDT) 
	- collects intensity measurements of scattered light 
	- 3D imaging technique 
- Issues: 
	- costly acquisition, imaging artifacts and high computational/memory requirements 
- forward model: y = A(x) + e
- image prior: x ~ p_x
- noise model: e ~ N(0, sigma^2(I)) also given by v
- sampling images from p_x is equivalent to obtaining a vector from a lower-dimensional and non-linear subset x of real numbers
- Maximum a posteriori probability (MAP) estimator motivates formulation as a composite optimization 
- Image denoising is an inverse problem that often can be related to the proximal operator 
- Plug and play priors (PnP) uses deep denoisers as image priors 
	- train the denoiser: 
		- add wide range of noise to image and train a neural network to try to remove the noise 
		- use tweedie's formula to get the information about the gradient 
- Blind inverse problems are those where the measurement operators are also unknown 
- Block coordinate plug and play methods for blind inverse problems 
	- theoretically converges for nonconvex data terms and expansive MMSE denoisers 
- traditional reconstruction methods fail on extreme limited angle computed tomography (LACT) 
- DOLCE is a model based generative network that uses a conditional image denoiser as a prior 
- Deep continuous artifact-free fields (DeCAF) reconstructs images represented continuously as a neural network 
- DeCAF represents the derived image continuously using an implicit neural representation (INR) 
## [Deep Generative Physical Modeling for Medical Imaging and Wireless Communications ](gaps_ideas.md#MIDAS_AI#gap1)
- multiple input multiple output communications 
- matrix of transmit and receive pairs, channel state information for good reliable communications 
- signal is the fourier transform of the image 
- collecting data = time consuming, common problem is to collect less data and then use generative AI to generate a better final image with lesser data 
- y = A(x); A is the random gaussian measurement function. x is the image
##### end to end supervised training
- trying to learn to invert the forward model with deep networks 
	- choosing ground truth is very important 
	- deep network is coupled to the measurement process (sampling pattern cant change in test)
	- deep network is tuned to perform well on knee if trained with knee data and on brain if trained with brain data, not generalized because so many parameters are tuned to the training set 
	- estimating uncertainty is hard
##### goal: estimate the image from noisy measurements 
- likelihood function: describe the imaging physics p(y|x)
- prior knowledge: probability distribution for the image p(x)
- multi constrast diffusion model 
- freeze the model and fine tune the hyperparameters for our particular imaging protocol 

## Foundation Models, Generative Models and Inverse Problems 
- multiresolution textual inversion: teaching new concepts to SD 

## Deep Networks and the mutiple manifold problem 
- model problem: sparse approximation 
	- recover sparse x_0 from observations y = Ax_0 
## Understanding diffusion model objectives from ELBO perspective 
- diffusion model tutorials from google
- most are based on a likelihood based models optimized towards minimizing the log likelihood ELBO 
- progressive distillation: to make sampling fasters