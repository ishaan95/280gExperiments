# Implementation notes
Order of package installations are important. This makes sense since each package installation would change the state of the environment a bit. In my case cudnn installation was messing up the matplotlib installation. However, installing it after matplotlib and tensorflow worked!

# Notes on VQVAE

## Background (10 mins)
Some background on the topics that have been covered in this seminar so far. This includes autoencoders, variational autoencoders and discrete variational autoencoders.  

### Autoencoders
An Autoencoder is a neural network that learns in an unsupervised manner (no labeled training data). A more appropriate description of autoencoders would be that it is self-supervised since the labels are learned. 

#### The encoder
This is a neural network which transforms input data into a low-dimensional space. 

#### The decoder

#### The latent space
The latent space is a low-dimension (compressed) representation of the input data.  

### Variational Autoencoders (VAE)
The difference in VAEs compared to vanilla autoencoders is the structure of the latent space. Here, data points close in the latent space would belong to the same cluster and data points far apart would belong to different clusters. 

### Discrete Variational Autoencoders
In VAEs the latent space is continuous (rather, a list of continuous functions)

## Vector Quantized Variational Autoencoder
In quantization (at least in the signal processing context), each value sampled from a continuous function is classified into buckets (based on how close it is to that single bucket value) such that the continuous function is transformed into a discrete function. A similar approach is applied here by using the codebook. 

### The Codebook component
The codebook is a list of vectors. Each vector is a quantization bucket. Therefore, each output of the encoder network is mapped to a codebook vector based on minimum eucledian distance. 

This quantized output (list of vectors) is then given to the decoder as input. The decoder then reconstructs the original image based on the list of vectors/

For images, the output of the quantizer would be a grid of vectors.

The codebook vectors as well as the encoder outputs are learnt by using gradient descent. This would mean that the loss function would include gradients of both the encoder output as well as a gradient of the codebook vector

### Training the prior


## Vector Quantized Variational Autoencoder - Part 2
In VQ-VAE-2, a hierarchy of encoders, decoders and vector quantizers are used. The decoders at the top and bottom levels then work together to reconstruct the image. 