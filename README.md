# gptransits

[![arXiv](https://img.shields.io/badge/arXiv-1908.10662-b31b1b.svg?style=flat)](https://arxiv.org/abs/1908.10662)
[![DOI](https://zenodo.org/badge/85022223.svg)](https://zenodo.org/badge/latestdoi/85022223)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

**Fit planetary transits and stellar signals at the same time with the help of gaussian processes**

## Installation
All python dependencies necessary for gptransits are available in pip (one of the package dependencies requires numpy to be installed beforehand). These can be seen in [setup.py](https://github.com/Fill4/gptransits/tree/master/setup.py).

*gptransits* can be installed from pip:
~~~ bash
pip install gptransits
~~~
Or from the source:
~~~ bash
git clone https://github.com/Fill4/gptransits.git
cd gptransits
python setup.py install
~~~

## Getting started
Script template (or ipython/jupyter notebook):
~~~ python
import gptransits

model = gptransits.Model("lightcurve_file.txt", "config_file.py")
model.run()
model.analysis(plot=True, fout="results_file.txt")
~~~

The model is initialized by providing a light curve file and a configuration file.
~~~ python
model = gptransits.Model("lightcurve_file.txt", "config_file.py")
~~~

The configuration file follows the structure in config_template.py. The available settings options can be seen in [settings.py](https://github.com/Fill4/gptransits/tree/master/gptransits/settings.py).  
The light curve file follows the format: 
~~~ 
#            time (days)              flux (frac)          flux_err (frac)
0.000000000000000000e+00 9.995755553299999763e-01 5.522560000000000197e-05
2.043337615740740618e-02 9.992535114099999616e-01 5.521756000000000196e-05
4.086675347222221838e-02 9.992965459599999489e-01 5.521029000000000160e-05
~~~

Running the MCMC algorithm to sample the posterior:
~~~ python
model.run()
~~~


Analysis calls a collection of functions that evaluate the MCMC convergence:
~~~ python
model.analysis(plot=True, fout="results_file.txt")
~~~
The plot flag defines if the analysis also creates some plots of interest, in a created figures folder.  
The fout flag, if defined, defines the file where the calculated results for the model parameters are saved.

Some examples ready to be run are available in the [examples](https://github.com/Fill4/gptransits/tree/master/examples) folder.  
Each folder has a light curve and a configuration file. Light curve files have the .lc extension.  
The output folder saves the chain and posterior probabilities from emcee in case the save flag is set in the configuration.  
The figures folder holds the plots from the analysis function.
