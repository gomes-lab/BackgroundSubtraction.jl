# BackgroundSubtraction.jl
A collection of background subtraction algorithms for spectroscopic data

# Getting Started 

After installing the latest version Julia and cloning this repository, please run 
`include("BackgroundSubtraction/src/install.jl")` in the Julia REPL.
This will install `BackgroundSubtraction.jl` along with a few dependencies that are not yet registered with Julia's package manager.

The main function is based on the [multi-component background learning model (MCBL)](https://rdcu.be/b32TH), with the corresponding function `mcbl`:
```
mcbl(A::AbstractMatrix, k::Int, x::AbstractVector, l::Real)
```
* `A` is the data matrix, each column of which is assumed to be a spectrogram.
* `k` is the number of components in the multi-component background model.
* `x` is the index vector corresponding to rows of `A`. 
For example, if a column of `A` is an X-ray diffraction spectrogram, `x` should be the angle of diffraction of each row.
* `l` is the length scale of the background component. It controls how quickly the 
background model is allowed to vary with `x`.
This functions as an important regularization for medium-sized data (100s-1000s spectrograms). 

There are 3 parameters controlling the algorithm, which can optionally be passed as keyword arguments:
* `minres` is the minimum residual standard deviation after which the algorithms terminates.
* `nsigma` is the number of standard deviations above the noise level after which a data point is classified as a peak. A smaller number will be more agressive in classifying points as peaks.
* `maxiter` is the maximum number of iterations between updating the noise and background model.

# Citing this work
If you use the MCBL for work or a publication, please cite [the original article](https://rdcu.be/b32TH):

Ament, Sebastian E., Helge S. Stein, Dan Guevarra, Lan Zhou, Joel A. Haber, David A. Boyd, Mitsutaro Umehara, John M. Gregoire, and Carla P. Gomes. "Multi-component background learning automates signal detection for spectroscopic data." npj Computational Materials 5, no. 1 (2019): 1-7.
https://doi.org/10.1038/s41524-019-0213-0	
