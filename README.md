# cmsmc_saturn

Axisymmetric Concentric Maclaurin Spheroid simulations of Saturn with Differential Rotation and Monte Carlo sampling.

## Synopsis

This code is provided as supplementary material for the article:

- Iess, L., Militzer, B., Kaspi, Y., Nicholson, P., Durante, D., Racioppa, P., … Zannoni, M. (2019). Measurement and implications of Saturn’s gravity field and ring mass. Science, (in Press).

It calculates self-consistent shape and gravitational field for interior structure
models of the planet Saturn.

It reflects the contributions of B. Militzer, S. M. Wahl and B. Hubbard to the
analysis contained in the sections on "Saturn interior models with uniform rotation"
and "Differential rotation on cylinders with the CMS method" in said paper.

The examples provided in this distribution are intended to demonstrate the
reproducibility of the model results presented in Figures 2 and 3, along with the
representative model presented in column 5 of Table 2.

## Requirements

We provide binary executable compiled on x86_64 Ubuntu Linux using the GNU c++
compiler (gcc version 5.2.0). And has been tested to work on similar Unix systems.

## Installation 

- Locate and download the [binary release](https://github.com/smwahl/cmsmc/releases).

- Uncompress the the ZIP file.

~~~bash
unzip cmsmc_release_linux_v1.0.zip
~~~

- You may need to change permissions on the executable file.

~~~bash
chmod +x cms
~~~

## Running the Code

The executable must be called from the command line with 9 input arguments:

~~~bash
./cms mode Tsid Rcore Smol Ymol Zmol Smet Ymet Zmet
~~~

### Input parameters

The model is described by two general physical parameters 

- Deep interior rotation period (`Tsid`) in seconds.
- Fractional radius of the core (`Rcore`).

The barotropic density profile is described by 6 parameters (3 for the outer,
molecular envelope, and 3 for the inner, metallic

- Entropy of outer envelope (`Smol`) in ***Units***
- Helium mass fraction of outer envelope (`Ymol`)
- Heavy element mass fraction of outer envelope (`Zmol`)
- Entropy of outer envelope (`Smet`) in ***Units***
- Helium mass fraction of outer envelope (`Ymet`)
- Heavy element mass fraction of outer envelope (`Zmet`)


The code can be run in two modes, specified using the parameter mode `mode`:

1. A single CMS simulation for a set of input parameters (`mode`= 0)

2. A Monte Carlo sampling of the parameter space (`mode` = 1), where the specified
   model conditions give the initial model for the Monte Carlo sampling.

   - The MC procedure updates the 6 barotrope parameters while holding the general
     physical parametes constant.
    
**Note: the Monte Carlo sampling is sensitive to the starting parameters and may fail
for some combination of inputs.**

For further discussion of these parameters and interior models can be found can be
found in the following references:

- Militzer, B., Soubiran, F., Wahl, S. M., & Hubbard, W. (2016). Understanding Jupiter ’s interior. Journal of Geophysical Research: Planets, 121, 1552–1572. http://doi.org/:10.1002/2016JE005080

- Wahl, S. M., Hubbard, W. B., Militzer, B., Guillot, T., Miguel, Y., Movshovitz, N., … Bolton, S. J. (2017). Comparing Jupiter interior structure models to Juno gravity measurements and the role of a dilute core. Geophysical Research Letters, 44(10), 4649–4659. http://doi.org/10.1002/2017GL073160

The interior models rely on equations of state for hydrogen helium mixtures, based on
ab-intio (DFT-MD) computer simulations, which are freely available
[here](http://militzer.berkeley.edu/HHe-EOS/)

### Example

We provide and example input in `example.scr`, which represents the parameters for
the representative model with a deep interior rotation rate of 10h39m22s (Column 5 of
Table 2 in the article). We also provide a corresponding output file
`output_example.txt' showing the expected output.

Here are the parameters appearing in `example.scr`

***Note: Placeholder values -- These will change in the submitted version***

~~~bash
./cms 1 0.2 38362.0 7.1976 0.2333 0.0169 7.1976 0.2333 0.0514 > output.txt
~~~

### Analyzing the Output

## Citation

To cite ***cmsmc*** or derived code in publications, please include the following
publications:

- Hubbard, W. B. (2013). Concentric Maclaurin Spheroid Models of Rotating Liquid Planets. The Astrophysical Journal, 768(1), 43. http://doi.org/10.1088/0004-637X/768/1/43

- Wahl, S. M., Hubbard, W. B., & Militzer, B. (2017). The Concentric Maclaurin Spheroid method with tides and a rotational enhancement of Saturn’s tidal response. Icarus, 282, 183–194. http://doi.org/10.1016/j.icarus.2016.09.011

Iess, L., et al. (2019). Measurement and implications of Saturn's gravity field and
ring mass. Science, in Press.

A Bibtex entry for _LaTeX_ users is:

~~~
@article{Hubbard2013,
author = {Hubbard, William B.},
doi = {10.1088/0004-637X/768/1/43},
file = {:Users/swahl/Documents/Mendeley Desktop/Hubbard/2013/Hubbard - 2013 - The Astrophysical Journal.pdf:pdf},
issn = {0004-637X},
journal = {Astrophys. J.},
month = {may},
number = {1},
pages = {43},
title = {{Concentric Maclaurin Spheroid Models of Rotating Liquid Planets}},
url = {http://stacks.iop.org/0004-637X/768/i=1/a=43?key=crossref.a31bd47c857111e805198695ba70780e},
volume = {768},
year = {2013}
}
@article{Wahl2017,
author = {Wahl, Sean M. and Hubbard, William B. and Militzer, Burkhard},
doi = {10.1016/j.icarus.2016.09.011},
eprint = {1602.07350},
file = {:Users/swahl/Documents/Mendeley Desktop/Wahl, Hubbard, Militzer/2017/Wahl, Hubbard, Militzer - 2017 - Icarus.pdf:pdf},
issn = {10902643},
journal = {Icarus},
pages = {183--194},
publisher = {Elsevier Inc.},
title = {{The Concentric Maclaurin Spheroid method with tides and a rotational enhancement of Saturn's tidal response}},
volume = {282},
year = {2017}
}
@article{Iess2019,
author = {Iess, L. and Militzer, B. and Kaspi, Y. and Nicholson, P. and Durante, D. and Racioppa, P. and Anabtaw, A. and Galanti, E. and Hubbard, W. and Mariani, M. J. and Tortora, P. and Wahl, S. M. and Zannoni, M.},
journal = {Science (80-. ).},
mendeley-groups = {Bibliographies/CMS papers},
title = {{Measurement and implications of Saturn's gravity field and ring mass}},
volume = {(in Press)},
year = {2019}
}
~~~
