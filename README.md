# Internal Linear Combination For Cosmic Microwave Background.


## This repository contains:

  1) Implementation of simple ILC (Internal Linear Combination) method (see (1), (2), (3), also one can find a chapter about ILC in the book (8)).
  2) Small example using [CMB](https://en.wikipedia.org/wiki/Cosmic_microwave_background) data from [Planck](https://en.wikipedia.org/wiki/Planck_(spacecraft)) experiment (see (4), (5)).
  3) Visualization using [HEALPix](https://en.wikipedia.org/wiki/HEALPix) (Hierarchical Equal Area isoLatitude Pixelation of a sphere) python package (see (6)).

## More information:

Separation of the main signal from noise is a challenging problem in analysis of cosmic microwave background ([CMB](https://en.wikipedia.org/wiki/Cosmic_microwave_background)) in [WMAP](https://en.wikipedia.org/wiki/Wilkinson_Microwave_Anisotropy_Probe) and [Planck](https://en.wikipedia.org/wiki/Planck_(spacecraft)) experiments.

ILC method, alongside with classical methods such as Wavelet analysis, ICA (Independent Component Analysis) and many others, is one of the most widely used approaches in data analysis in Cosmology. The goal of this repository is to show that even simple version of ILC produces satisfactory results for the problem.

#### Below are a few words about ILC.

[WMAP](https://en.wikipedia.org/wiki/Wilkinson_Microwave_Anisotropy_Probe) and [Planck](https://en.wikipedia.org/wiki/Planck_(spacecraft)) experiments created a full-sky map of [CMB](https://en.wikipedia.org/wiki/Cosmic_microwave_background) (electromagnetic radiation remnant from an early stage of the Universe) via multi-frequency observation. 

The data consists of several maps in HEALPix format. There are separate files for different frequencies. Each file contains pixels with temperatures.

Supose that for some map in channel i at pixel p we have

![](https://latex.codecogs.com/gif.latex?S%5E%7B%28i%29%7D%28p%29%20%3D%20%5COmega_%7BCMB%7D%20%5E%7B%28i%29%7D%28p%29%20&plus;%20S%5E%7B%28i%29%7D_%7Bf%7D%28p%29%20&plus;%20%5Cmathcal%7BN%7D%5E%7Bi%7D%28p%29)

where  

![](https://latex.codecogs.com/gif.latex?%5COmega_%7BCMB%7D%20%5E%7B%28i%29%7D%28p%29) - CMB contribution, which we want to find,

![](https://latex.codecogs.com/gif.latex?S%5E%7B%28i%29%7D_%7Bf%7D%28p%29) - diffuse Galactic foreground contribution, which influence we want to reduce,  

![](https://latex.codecogs.com/gif.latex?%5Cmathcal%7BN%7D%5E%7Bi%7D%28p%29) -  the experimental noise.

Example picture for one of the channels with applied mask: 

![image](https://user-images.githubusercontent.com/48928457/74084186-bbc77580-4a7d-11ea-83be-5e417a2fc3d9.png)

The main assumption for ILC is that CMB contribution does not depend on channel. Then the observed map is

![](https://latex.codecogs.com/gif.latex?S%5E%7B%28i%29%7D%28p%29%20%3D%20%5COmega_%7BCMB%7D%28p%29%20&plus;%20S%5E%7B%28i%29%7D_%7Bf%7D%28p%29%20&plus;%20%5Cmathcal%7BN%7D%5E%7Bi%7D%28p%29)

Using these maps we need to estimate CMB contribution.
One can search for a solution in the form of weighted linear combination, with the weights independent from p: 

![](https://latex.codecogs.com/gif.latex?%5Cwidetilde%7B%5COmega%7D_%7BCMB%7D%28p%29%20%3D%20%5Csum_%7Bi%3D1%7D%5E%7BN_a%7D%20%5Comega_i%20S%5E%7B%28i%29%7D%28p%29)

Also we imply the constraint 

![](https://latex.codecogs.com/gif.latex?%5Csum_%7Bi%3D1%7D%5E%7BN_a%7D%20%5Comega_i%20%3D%201) 

In this case, one can write the estimated component as

![](https://latex.codecogs.com/gif.latex?%5Cwidetilde%7B%5COmega%7D_%7BCMB%7D%28p%29%20%3D%20%5COmega_%7BCMB%7D%28p%29%20&plus;%20%5Csum_%7Bi%3D1%7D%5E%7BN_a%7D%20%5Comega_i%20%5Cleft%28%20S%5E%7B%28i%29%7D_%7Bf%7D%28p%29%20&plus;%20%5Cmathcal%7BN%7D%5E%7Bi%7D%28p%29%20%5Cright%29)

The weights have to minimize the variance:

![](https://latex.codecogs.com/gif.latex?%5C%7B%5Comega_i%5C%7D%20%3D%20%5Coperatorname*%7Bargmin%7D_%7B%5C%7B%5Comega_i%5C%7D%7D%20%5Cleft%28%20Var%5Cleft%5B%5COmega_%7BCMB%7D%28p%29%5Cright%5D%20&plus;%20Var%5Cleft%5B%5Csum_%7Bi%3D1%7D%5E%7BN_a%7D%20%5Comega_i%20%5Cleft%28%20S%5E%7B%28i%29%7D_%7Bf%7D%28p%29%20&plus;%20%5Cmathcal%7BN%7D%5E%7Bi%7D%28p%29%20%5Cright%29%20%5Cright%5D%5Cright%20%29)

The solution of this problem is 

![](https://latex.codecogs.com/gif.latex?%5Comega_i%20%3D%20%5Cfrac%7B%5Csum_%7Bj%3D1%7D%5E%7Bk%7DC%5E%7B-1%7D_%7Bij%7D%7D%7B%5Csum_%7Bl%3D1%7D%5E%7Bk%7D%5Csum_%7Bj%3D1%7D%5E%7Bk%7DC%5E%7B-1%7D_%7Blj%7D%7D)

where C is covariance matrix:

![](https://latex.codecogs.com/gif.latex?C_%7Bij%7D%20%3D%20%5Clangle%20%5CDelta%20S_i%20%5CDelta%20S_j%5Crangle)

## Comparison of the official map with the map received by our code:
  1) Official CMB map by Planck experiment
  2) Current code output map

![Annotation 2020-01-27 150948](https://user-images.githubusercontent.com/46852371/73173740-1fb17c00-4117-11ea-83a2-52c6fae0467c.jpg)


## Links and papers: 

  1)  https://arxiv.org/pdf/0806.0520.pdf A Statistical Analysis of the "Internal Linear Combination" Method in Problems of Signal Separation as in CMB Observations (R. Vio and P. Andreani, 2008)
  
  2)  https://arxiv.org/pdf/0811.4277.pdf "Internal Linear Combination" method for the separation of CMB
from Galactic foregrounds in the harmonic domain (R. Vio and P. Andreani, 2008)

  3)  https://arxiv.org/pdf/astro-ph/0403098.pdf On Foreground Removal From The Wilkinson Microwave Anisotropy Probe Data By An Internal Linear Combination Method: Limitations And Implications (H. K. Eriksen et al, 2004)
  
  4)  https://lambda.gsfc.nasa.gov/product/map/dr5/ilc_map_info.cfm 
      https://lambda.gsfc.nasa.gov/toolbox/tb_comp_separation.cfm Information about usage of ILC in WMAP experiment
  
  5)  https://irsa.ipac.caltech.edu/data/Planck/release_2/all-sky-maps/ Public download link for CMB maps

  6)  https://healpix.sourceforge.io/
      https://github.com/healpy/healpy Hierarchical Equal Area isoLatitude Pixelation of a sphere project website
      
  7)  https://arxiv.org/pdf/0802.0400.pdf A Modified ICA Approach for Signal Separation in CMB Maps (R. Vio and P. Andreani, 2008)
  
  8)  https://www.springer.com/gp/book/9783540239727 Data Analysis in Cosmology (V.J. Martinez et al, Springer 2009)
