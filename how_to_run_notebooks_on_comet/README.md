# Using Jupyter Notebooks on the SDSC Comet Cluster
**By** [Mary Thomas, SDSC](https://www.sdsc.edu/research/researcher_spotlight/thomas_mary.html)
**Updated:**  July 28, 2021

This quick-start guide will show you how to run jupyter notebooks on Comet using the [SDSC Reverse Proxy Service (RPS)](https://hpc-training.sdsc.edu/notebooks-101/notebook-101.html). RPS is a prototype system that will allow users to launch secure (HTTPS) Jupyter Services on on any Comet compute node using a simple bash script called *start_notebook*. The notebooks will be made available to the user outside of the cluster firewall using a *secure* HTTPS connection between the external users web browser and the reverse proxy server.

## Set up a SECURE (HTTPS) Jupyter Notebook environment on Comet:

SDSC recommends that you install the *Miniconda* Jupyter notebook environment on its HPC systems and that you create a Conda Virtual Environment. The tutorial below provides full instructions on how to do this.
* [Running Notebooks on Comet](https://hpc-training.sdsc.edu/notebooks-101/notebook-101.html)
* [Setting up a Conda Virtual Environment](https://hpc-training.sdsc.edu/notebooks-101/notebook-101.html#software-prerequisites)

Once your notebook environment is working, follow the steps below:

## Log onto comet.sdsc.edu  
For more help, see https://github.com/sdsc-hpc-training-org/basic_skills/tree/master/connecting-to-hpc-systems
```
ssh -Y -l <username> comet.sdsc.edu
```

## Create a test directory
Clone the notebook example repository, or use one you have already created
* [SDSC HPC Notebook Examples](https://github.com/sdsc-hpc-training-org/notebook-examples)
```
git clone https://github.com/sdsc-hpc-training-org/notebook-examples.git
```

## Launch the secure notebook Using the *Reverse Proxy Service*
```
start-notebook
```
For more information on using ```start-notebook``` including configuration and installation, see https://comet-notebooks-101.readthedocs.io/en/comet/methods/reverseProxy.html


