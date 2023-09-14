- Diffusion Based Generative Models 
	- Image generation 
		- DALL-E 2 2022
		- stable diffusion 2022
		- midjourney 2022
	- RFDiffusion 
	- Genie 2023
- Data is iteratively corrupted with (like Gaussian noise) noise (random prior or forward diffusion) and a model learns to de-noise or reverse diffusion process. 
	- reverse diffusion process is the learning process
	- nothing is learnt during the forward diffusion process
### Forward Diffusion Process
- adds gaussian noise (random) to the image 
	- leads to random prior data 
	- Markov Chain of T time steps (t = 0 to t = T)
	- q(x): distribution of images of landscapes if thats what we're trying to regenerate
	- x_t: matrices describing the image at different time steps (t) in forward diffusion 
	- ![[recurssive_gaussian_noise.png]]
	- second term (E_t-1) is adding noise to the previous image (x_t-1)
		- the noise we're adding is isotropic. using an identity matrix (N). the pixels are treated individually and noise is not correlated between pixels 
	- can jump in noise time steps using alpha_t = 1 - Beta_t and alpha bar (multiplication of all alpha_ts). can get a noisy image at any time step when using alpha_t
	- Variance Beta schedule (Beta_t: important hyper parameter that controls adding noise) 
		- linear Beta schedule: linearly adding noise (increasing Beta_t) over time
		- quadratic Beta schedule
		- cosine Beta schedule: performs the best
		- how many time steps are needed for the sampling? 1000s 
			- these are slow compared to VAEs 
### Reverse Diffusion 
- removing noise from the random prior 
- sampling x_t (corrupted image) from a distribution (q_t(x_t|x_0))
- we can add nose in many many ways. so we generate a noise sample from our clean sample in the forward diffusion 
	- we try to get a new sample from the noise sample in reverse diffusion 
		- can we generate a new sample from the noisy sample? 
		- answer is hidden in the 
			(1) epsilon of the forward diffusion equation 
			this epsilon is found using neural networks. we are tying to predict how much noise was added to the image 
			(2) x_0 
			what does the true image (original sample) look like? the model can compute how much noise was added 
- How do we do the learning process?
	- Training Objective (ELBO)
		- three terms in the equation includes a reconstruction term (how well are we able to reconstruct the data?), prior term (when we completely noise our data, does that distribution look like the true prior/gaussian distribution?) and denoising step term (we're going from time step t and we want to denoise it (t-1); how well are we doing that step?)
		- aim to optimize: the denoising step term 
			- Ho et al. 2020 uses MSE (mean square error loss) loss on Predicted Noise as the loss function (grading the gradient decent)
#### Algorithms for training the reserve
- why would the model diffuse towards the right trajectory?
	- sampling (inference)
		- take a sample from our prior distribution 
		- sample our noise and compute predicted noise (epsilon of teta)
		- take a small step to remove that predicted noise 
	- training 
		- get example from data set and get time
		- get noise (epsilon)
		- take gradient descent step on noise until time t and compute loss (MSE) 
		- until converged 