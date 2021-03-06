# Bayeslands Workshop

*Part of the Badlands (Basin and landscape Dynamics) suite* from the The University of Sydney  .

These materials are designed to give you a brief introduction to the Badlands (BAsin nD LANdscape DynamicS) modelling code, extended functionality provided by pyBadlands, the Bayesian inference methods in Bayeslands, and additional helper tools. 
See https://github.com/badlands-model/pyBadlands and the repositories therin for details on various Badlands/Bayeslands incantations.

[email us](mailto:nathaniel.butterworth@sydney.edu.au)


## Installation

This repo is at http://github.com/badlands-model/Bayeslands-Workshop


### Via Docker

The easiest way to install and run the **Bayeslands Workshop** is by downloading through Docker.

Download the [dockerfile](Docker_details/Dockerfile) 

Change into the folder with the docker file, then execute:

``` 
docker build -t bayeslands . 
```

Then to run, execute:

```
docker run -p 8888:8888 bayeslands
```

From there, launch a web browser on your local machine, navigate to 0.0.0.0:8888 and you can explore the folder structure within the Jupyter notebook environment. Click on the StartHere.ipynb for some instructions! Note, you may need to use the --no-cache flag in the docker build command to re-download the git repository and install a up-to-date copy.


### Via Compile

Or download the repo and compile pyBadlands.

```
git clone https://github.com/badlands-model/Bayeslands_Workshop.git
cd Bayeslands_Workshop/pyBadlands/libUtils
make 
cd -
pip install -e Bayeslands_Workshop
```

#### Dependecies for compiliation

If you compile this workshop locally, then several dependencies (easily installed with anaconda and pip) are required. These steps should get you an evironment ready to compile pyBadlands (above).

```
conda create --name pybad python=2.7.13 
source activate pybad
conda install jupyter h5py markupsafe numba=0.35.0 singledispatch backports_abc certifi jsonschema ipyparallel
conda install path.py matplotlib=2.0.2 pandas scipy=0.19.1 basemap=1.0.7 mpi4py plotly  Cython==0.20 
conda install PIL  
pip install ez_setup colorlover cmocean scikit-fuzzy pyevtk zmq git+https://github.com/badlands-model/triangle

git clone https://github.com/awickert/gFlex.git 
cd gFlex/
python setup.py install
cd ..
```


## Workshop

Following the notebooks in order will guide you through understanding how the Badlands and Bayeslands models are built and executed. Hopefully you should be able to replace these example datasets with your own workflows.


### Building input

These notebooks will help you to create surface grids for generic, real (based on etopo1) topographic/bathymetric datasets.

* [Generic Surface](Examples/topoCreate.ipynb): generic surface generation notebook.
* [etopo1 Surface](Examples/etopoGen.ipynb): etopo1 surface generation notebook.


### Running Badlands and Bayeslands

We provide a full examples that create a surface and then runs multiple simulations to estimate uncertainties in your parameter selections.

* [Badlands Mountain Example](Examples/mountain.ipynb): running a standard Badlands model.
* [Bayeslands Crater Surface](Examples/bl_topogenr.ipynb): create a surface to run and test models against.
* [Bayeslands Crater Example](Examples/bl_mcmc.ipynb): run bayesian inference on a badlands model.
* [PT Bayeslands Crater Example](Examples/ptBayeslands.ipynb): surface to run and test models against using parallel tempering.

Additional [theory on Bayseian methods](Bayeslands_Workshop2018.pdf).
 
### Post-processing and other tools

Many post processing analysis steps can be done to produce various figures and interrogate different parts of the numerical model.

* [Likelihood surface creation](Examples/bl_surflikl.ipynb): explores the the parameter space in evaluating the model.


# Additional notes

## Badlands, Bayeslands, What?

**Badlands** is the code (originally written in Fortran) to model surface processes.

**pyBadlands** was an extension to Badlands that allowed for easy manipulation of model parameters, input files, execution, etc via the Python programming language.

**Bayeslands** uses pyBadlands and applies Bayesian inference to the Badlands models to essentially provide estimates of error. It runs 1000's of Badlands models with slightly different parameter choices, and compares the results against a 'known' solution to estimate an error. There are different versions of Bayeslands being developed that use different techniques (paralleltempering, surrogate assissted) to optimise accuracy and exploration efficiency in the models with different trade-offs.

## Papers

#### Bayeslands https://arxiv.org/abs/1805.03696
#### Parallel Tempering Bayeslands https://arxiv.org/abs/1806.10939

### Links 

[Jupyter Notebooks](http://www.jupyter.org)  
[Bayes, Probability, and Statistics](https://towardsdatascience.com/basic-probability-theory-and-statistics-3105ab637213)
