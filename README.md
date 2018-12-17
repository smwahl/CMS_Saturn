# CMS_Saturn

Axisymmetric Concentric Maclaurin Spheroid simulations of Saturn with Differential Rotation and Monte Carlo sampling.

## Synopsis

This code is provided as supplementary material for the article:

- Iess, L., Militzer, B., Kaspi, Y., Nicholson, P., Durante, D., Racioppa, P.,  Anabtaw, A., Galanti, E., Hubbard, W., Mariani, M. J., Tortora, P., Wahl, S. M., Zannoni, M. (2019). Measurement and implications of Saturn’s gravity field and ring mass. Science, (in Press).

It calculates self-consistent shape and gravitational field for interior structure
models of the planet Saturn.

It reflects the contributions of B. Militzer, S. M. Wahl and B. Hubbard to the
analysis contained in the sections on "Saturn interior models with uniform rotation"
and "Differential rotation on cylinders with the CMS method" in said paper.

## Requirements

We provide two binary executables: one compiled on x86_64 Ubuntu Linux using the GNU
c++ compiler (gcc version 5.2.0). The other was compiled on MacOS 10.14.2 (gcc version 4.2.1).

## Installation 

- Locate and download the [binary release](https://github.com/smwahl/cmsmc/releases).

- Uncompress the ZIP file.

~~~bash
unzip CMS_Saturn_v1.0.zip
~~~

- You may need to change permissions on the executable files.

~~~bash
chmod +x cms_Linux cms_osx
~~~

## Running the Code

Select the correct executable for your system `cms_Linux` or `cms_osx`.

The program is executed with the command:

~~~bash
./cms file=initial_models.txt iModel=random runMC
~~~

This begins a Monte Carlo search of cms models starting from one of 11 starting
models included in `initial_models.txt`. A sample output text file is included for
this in `reference_output.txt`.

### Command-line arguments

The CMS model is initialized to a set of starting conditions contained in a text
file. The argument `file=initial_models.txt` specifies this file, and the argument
`iModel` selects which model to start the simulation with (e.g. `iModel=5`).
`iModel=random` will choose one of the starting models at random.


The model is described by two general physical parameters 

- Deep interior rotation period, `P`, in hours:minutes:seconds (default = 10:39:22.4).
- Fractional radius of the core, `rCore` (default = 0.2).

The code can then be ran for each value presented in the article using:

~~~bash
./cms file=initial_models.txt iModel=random runMC rCore=0.188
./cms file=initial_models.txt iModel=random runMC rCore=0.231
./cms file=initial_models.txt iModel=random runMC P=10:32:44
./cms file=initial_models.txt iModel=random runMC P=10:39:22.4
./cms file=initial_models.txt iModel=random runMC P=10:45:45
./cms file=initial_models.txt iModel=random runMC P=10:47:06
~~~

The code will run two initial calculations
    
1. An initial simulation with the parameters in the input file.
2. A series of calculations attempting to fit the target value for J_2 using the 

If the flag `runMC` is omitted the code will then stop at this point; if `runMC` is
included it will proceed to run Monte Carlo sampling with the 

### Model parameters

The MC sampling samples a set of parameters for the interior structure of the CMS
saturn models.
The barotropic density profile is described by 8 parameters describing conditions in
the outer, molecular envelope, the inner, metallic envelope, and the transition
between the two states

- Entropy of outer envelope (`S1`) in S/kB/Ne
- Helium mass fraction of outer envelope (`Y1`)
- Heavy element mass fraction of outer envelope (`Z1`)
- Entropy of outer envelope (`S2`) in S/kB/Ne
- Helium mass fraction of outer envelope (`Y2`)
- Heavy element mass fraction of outer envelope (`Z2`)
- Pressure of the top of the helium rain layer (`PSwitch1`)
- Pressure of the bottom of the helium rain layer (`PSwitch2`)

Finally, the models have profile of differential rotation (`omega`) described by fraction of
the deep rotation rate (`P`) as a function of distance from the rotational axis. A
uniformly rotating planet would, thus be described with:

~~~bash
omega= +1.0 +1.0 +1.0 +1.0 +1.0 +1.0
~~~

**Note: the Monte Carlo sampling is sensitive to the starting parameters and may fail
for some combination of inputs.**

For further discussion of these parameters and interior models can be found can be
found in the following references:

- Militzer, B., Soubiran, F., Wahl, S. M., & Hubbard, W. (2016). Understanding Jupiter ’s interior. Journal of Geophysical Research: Planets, 121, 1552–1572. http://doi.org/:10.1002/2016JE005080

- Wahl, S. M., Hubbard, W. B., Militzer, B., Guillot, T., Miguel, Y., Movshovitz, N., … Bolton, S. J. (2017). Comparing Jupiter interior structure models to Juno gravity measurements and the role of a dilute core. Geophysical Research Letters, 44(10), 4649–4659. http://doi.org/10.1002/2017GL073160

The interior models rely on equations of state for hydrogen helium mixtures, based on
ab-intio (DFT-MD) computer simulations, which are freely available
[here](http://militzer.berkeley.edu/HHe-EOS/)

## Analyzing the Output

Over the course of the simulation the code output's the state of the simulation. The
output includes the model parameters

~~~
CMS finished: chi2= 0.3061849421 for  MC Parameters: S1=  +6.8416240000 Y1=  +0.2652640273 Z1=  +0.0118391310 S2=  +7.1056362659 Y2=  +0.2781065949 Z2=  +0.0323756282 PSwitch1=  +78.9406658821 PSwitch2=  +103.2695309206 omega= +0.9913867210 +0.9948385058 +1.0044704847 +1.0250106842 +1.0390679124 +1.0447764244
~~~

and a comparison of the calculated and observed (target) gravitational harmonics
J_n.

~~~
Target:         J2= 16290.5510 J4=  -935.2490 J6=    86.3580 J8=   -14.5390 J10=     4.7750
Final: Jn*10^6: J2= 16290.5511 J4=  -935.2340 J6=    86.3283 J8=   -14.7986 J10=     4.7767 J12=    -1.4177 J14=   0.146974 J16=   0.028970
~~~

Prior to the start of the monte carlo sampling the the state of the initial CMS
calculation is noted by:

~~~
Very first CMS run was successful for:
~~~

And the state of the model upon the inital fit to J2 is denoted by

~~~
Matched J2
~~~

### Monte Carlo Sampling

Output from the Monte Carlo sampling begins after 

~~~
 ======= Starting MC chain =======
~~~

During the sampling the algorithm attempts changes to one of each model parameter,
and either accepts or rejects the model with:

~~~
 :::: ACCEPTED ::::  s= 0 i= 2 chi2= 0.660028312 chi2New= 0.6897556611
~~~

or

~~~
 :::: REJECTED ::::  s= 0 i= 6 chi2= 0.7558173591 chi2New= 1.840898714
~~~

The current state of the parameters is then displayed as

~~~
 :::: STATE ::::  chi2= 0.7558173591  MC Parameters: S1=  +6.8416240000 Y1=  +0.2652640273 Z1=  +0.0119143034 S2=  +7.1056362659 Y2=  +0.2781065949 Z2=  +0.0323756282 PSwitch1=  +79.0272519051 PSwitch2=  +103.1830952493 omega= +0.9913867210 +0.9948385058 +1.0046551844 +1.0250106842 +1.0382056094 +1.0457426337
~~~

Where `chi2` quantifies the difference between the calculated and observed (target)
gravitational harmonics, $J_n$. The individal harmonics are once again desplayed.

~~~
 Target:         J2= 16290.5510 J4=  -935.2490 J6=    86.3580 J8=   -14.5390 J10=     4.7750
 Final: Jn*10^6: J2= 16290.5511 J4=  -936.1244 J6=    86.6531 J8=   -14.8042 J10=     4.6867 J12=    -1.3443 J14=   0.121533 J16=   0.022133
~~~

## Citation

To cite ***CMS_Saturn*** or derived code in publications, please include the following
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
