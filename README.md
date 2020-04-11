# Internal Linear Combination For Cosmic Microwave Background.


## This repository contains:

  1) Implementation of ILC (Internal Linear Combination) method (see (1), (2), (3), also one can find a chapter about ILC in the book (8)).
  2) Small example using CMB data from Planck  experiment (see (4), (5)).
  3) Visualization using HEALPix (Hierarchical Equal Area isoLatitude Pixelation of a sphere) python package (see (6)).

## More information:

Separation of the main signal from noise is a challenging problem in analysis of cosmic microwave background (CMB) in WMAP and Planck experiments.

ILC method, alongside with classical methods such as Wavelet analysis, ICA (Independent Component Analysis) and many others, is one of the most widely used approaches in data analysis in Cosmology.

Below are a few words about ILC.

WMAP and Planck experiments created a full-sky map of CMB (electromagnetic radiation remnant from an early stage of the Universe) via multi-frequency observation. The data consists of 
Supose for channel i at pth pixel we have 

![](https://latex.codecogs.com/gif.latex?S%5E%7B%28i%29%7D%28p%29%20%3D%20%5COmega_%7BCMB%7D%20%5E%7B%28i%29%7D%28p%29%20&plus;%20S%5E%7B%28i%29%7D_%7Bf%7D%28p%29%20&plus;%20%5Cmathcal%7BN%7D%5E%7Bi%7D%28p%29)

where  

![](https://latex.codecogs.com/gif.latex?%5COmega_%7BCMB%7D%20%5E%7B%28i%29%7D%28p%29) -- CMB contribution

![](https://latex.codecogs.com/gif.latex?S%5E%7B%28i%29%7D_%7Bf%7D%28p%29) -- diffuse Galactic foreground contribution  

![](https://latex.codecogs.com/gif.latex?%5Cmathcal%7BN%7D%5E%7Bi%7D%28p%29) --  the experimental noise

Example picture one of the channels: 

![image](https://user-images.githubusercontent.com/48928457/74084186-bbc77580-4a7d-11ea-83be-5e417a2fc3d9.png)

The main assumption for ILC that CMB contribution does not depend on channel

![](https://latex.codecogs.com/gif.latex?S%5E%7B%28i%29%7D%28p%29%20%3D%20%5COmega_%7BCMB%7D%28p%29%20&plus;%20S%5E%7B%28i%29%7D_%7Bf%7D%28p%29%20&plus;%20%5Cmathcal%7BN%7D%5E%7Bi%7D%28p%29)

So try to find solution in this form: 

![](https://latex.codecogs.com/gif.latex?%5Cwidetilde%7B%5COmega%7D_%7BCMB%7D%28p%29%20%3D%20%5Csum_%7Bi%3D1%7D%5E%7BN_a%7D%20%5Comega_i%20S%5E%7B%28i%29%7D%28p%29)

If we use constraint 

![](https://latex.codecogs.com/gif.latex?%5Csum_%7Bi%3D1%7D%5E%7BN_a%7D%20%5Comega_i%20%3D%201) 

then 

![](https://latex.codecogs.com/gif.latex?%5Cwidetilde%7B%5COmega%7D_%7BCMB%7D%28p%29%20%3D%20%5COmega_%7BCMB%7D%28p%29%20&plus;%20%5Csum_%7Bi%3D1%7D%5E%7BN_a%7D%20%5Comega_i%20%5Cleft%28%20S%5E%7B%28i%29%7D_%7Bf%7D%28p%29%20&plus;%20%5Cmathcal%7BN%7D%5E%7Bi%7D%28p%29%20%5Cright%29)

The weights should be found by solving this problem: 

![](https://latex.codecogs.com/gif.latex?%5C%7B%5Comega_i%5C%7D%20%3D%20%5Coperatorname*%7Bargmin%7D_%7B%5C%7B%5Comega_i%5C%7D%7D%20%5Cleft%28%20Var%5Cleft%5B%5COmega_%7BCMB%7D%28p%29%5Cright%5D%20&plus;%20Var%5Cleft%5B%5Csum_%7Bi%3D1%7D%5E%7BN_a%7D%20%5Comega_i%20%5Cleft%28%20S%5E%7B%28i%29%7D_%7Bf%7D%28p%29%20&plus;%20%5Cmathcal%7BN%7D%5E%7Bi%7D%28p%29%20%5Cright%29%20%5Cright%5D%5Cright%20%29)

Solution is 

![](https://latex.codecogs.com/gif.latex?%5Comega_i%20%3D%20%5Cfrac%7B%5Csum_%7Bj%3D1%7D%5E%7Bk%7DC%5E%7B-1%7D_%7Bij%7D%7D%7B%5Csum_%7Bl%3D1%7D%5E%7Bk%7D%5Csum_%7Bj%3D1%7D%5E%7Bk%7DC%5E%7B-1%7D_%7Blj%7D%7D)

where

![](https://latex.codecogs.com/gif.latex?C_%7Bij%7D%20%3D%20%5Cleft%20%5Clangle%20%5CDelta%20T_i%20%5CDelta%20T_j%20%5Cright%20%5Crangle%20%3D%20%5Cfrac%7B1%7D%7BN_%7Bpix%7D%7D%20%5Csum_%7Bp%3D1%7D%5E%7BN_%7Bpix%7D%7D%20%28T_i%28p%29%20-%20%5Coverline%7BT_i%7D%29%28T_j%28p%29%20-%20%5Coverline%7BT_j%7D%29)

## Comparison of the official map with the map received by our code:
  1) Official CMB map by Planck experiment
  2) Current code output map

![Annotation 2020-01-27 150948](https://user-images.githubusercontent.com/46852371/73173740-1fb17c00-4117-11ea-83a2-52c6fae0467c.jpg)


## Links and articles: 

  1)  https://arxiv.org/pdf/0806.0520.pdf A Statistical Analysis of the "Internal Linear Combination" Method in Problems of Signal Separation as in CMB Observations R. Vio and P. Andreani 2008
  
  2)  https://arxiv.org/pdf/0811.4277.pdf "Internal Linear Combination" method for the separation of CMB
from Galactic foregrounds in the harmonic domain R. Vio and P. Andreani 2008

  3)  https://arxiv.org/pdf/astro-ph/0403098.pdf ON FOREGROUND REMOVAL FROM THE WILKINSON MICROWAVE ANISOTROPY PROBE DATA BY
AN INTERNAL LINEAR COMBINATION METHOD: LIMITATIONS AND IMPLICATIONS H. K. Eriksen et al 2004
  
  4)  https://lambda.gsfc.nasa.gov/product/map/dr5/ilc_map_info.cfm 
      https://lambda.gsfc.nasa.gov/toolbox/tb_comp_separation.cfm Information about usage of ILC in WMAP experiment
  
  5)  https://irsa.ipac.caltech.edu/data/Planck/release_2/all-sky-maps/ Public download link for CMB maps

  6)  https://healpix.sourceforge.io/
      https://github.com/healpy/healpy/Hierarchical Equal Area isoLatitude Pixelation of a sphere project website
      
  7)  https://arxiv.org/pdf/0802.0400.pdf A Modified ICA Approach for Signal Separation in CMB Maps R. Vio and P. Andreani 2008
  
  8)  https://www.springer.com/gp/book/9783540239727 V.J. Martinez et al, Data Analysis in Cosmology, Springer 2009
