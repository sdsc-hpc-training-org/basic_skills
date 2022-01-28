# Using Jupyter Notebooks on the SDSC Expanse Cluster
**By** [Mary Thomas, SDSC](https://www.sdsc.edu/research/researcher_spotlight/thomas_mary.html)
**Updated:**  July 28, 2021

## [Contents](#top)
* [Using the galyleo script](#galyleo)
* [Using the start-notebook script](#stntbk)
* [Notebook Examples](#ntbk-ex)

This quick-start guide will show you how to run jupyter notebooks on Expanse using the [SDSC Satellite Reverse Proxy Service (RPS)](https://hpc-training.sdsc.edu/notebooks-101/notebook-101.html). Satellite is a prototype system that will allow users to launch secure (HTTPS) Jupyter Services on any Expanse compute node using a simple bash script called *galyleo* or *start_notebook*. The notebooks will be made available to the user outside of the cluster firewall using a *secure* HTTPS connection between the external users web browser and the reverse proxy server.

_______
## Using the galyleo script 
[galyleo](https://github.com/mkandes/galyleo) is a shell utility to help you launch Jupyter notebooks on high-performance computing (HPC) systems in a simple, secure way. It works with the Satellite reverse proxy service and a batch job scheduler like Slurm to provide each Jupyter notebook server you start with its own one-time, token-authenticated HTTPS connection between the compute resources of the HPC system the notebook server is running on and your web browser. This HTTPS-secured connection affords both privacy and integrity to the data exchanged between the notebook server and your browser, helping protect you and your work against network eavesdropping and data tampering.

For details on using ```galyleo,``` see:  https://github.com/mkandes/galyleo

_______
## Using the start_notebook script 
Note: the *start_notebook* scripting system will be deprecated and replaced with the newer *galyleo* script

### Set up a SECURE (HTTPS) Jupyter Notebook environment on Expanse:

SDSC recommends that you install the *Miniconda* Jupyter notebook environment on its HPC systems and that you create a Conda Virtual Environment. The tutorial below provides full instructions on how to do this.
* [Running Notebooks on Expanse](https://hpc-training.sdsc.edu/notebooks-101/notebook-101.html)
* [Setting up a Conda Virtual Environment](https://hpc-training.sdsc.edu/notebooks-101/notebook-101.html#software-prerequisites)

Once your notebook environment is working, follow the steps below:

### Log onto Expanse
For more help, see https://github.com/sdsc-hpc-training-org/basic_skills/tree/master/connecting-to-hpc-systems
```
ssh -Y -l <username> login.expanse.sdsc.edu
```

______
### Using Example Notebooks<a name="ntbk-ex">
Clone the notebook example repository, or use one you have already created
* [SDSC HPC Notebook Examples](https://github.com/sdsc-hpc-training-org/notebook-examples)
```
git clone https://github.com/sdsc-hpc-training-org/notebook-examples.git
```

## Launch the secure notebook Using the *Satellite Reverse Proxy Service*
```
start-notebook
```
For more information on using ```start-notebook``` including configuration and installation, see https://comet-notebooks-101.readthedocs.io/en/comet/methods/reverseProxy.html


