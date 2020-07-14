# Using Jupyter Notebooks on the SDSC Comet Cluster
**By** [Mary Thomas, SDSC](https://www.sdsc.edu/research/researcher_spotlight/thomas_mary.html)
**Updated:**  July 14, 2020

This quick-start guide will show you how to run jupyter notebooks on Comet using the [SDSC Reverse Proxy Service (RPS)](https://comet-notebooks-101.readthedocs.io/en/comet/methods/reverseProxy.html). RPS is a prototype system that will allow users to launch secure (HTTPS) Jupyter Services on on any Comet compute node using a simple bash script called *start_notebook*. The notebooks will be made available to the user outside of the cluster firewall using a *secure* HTTPS connection between the external users web browser and the reverse proxy server.

## Set up a SECURE (HTTPS) Jupyter Notebook environment on Comet:

SDSC recommends that you install the *Miniconda* Jupyter notebook environment on its HPC systems and that you create a Conda Virtual Environment. The tutorial below provides full instructions on how to do this.
* [Running Notebooks on Comet](https://comet-notebooks-101.readthedocs.io/en/comet/index.html)
* [Setting up a Conda Virtual Environment](https://comet-notebooks-101.readthedocs.io/en/comet/prerequisites.html#setup-a-conda-virtual-environment)

Once your notebook environment is working, follow the steps below:

## Log onto comet.sdsc.edu  
For more help, see https://github.com/sdsc-hpc-training-org/basic_skills/tree/master/connecting-to-hpc-systems
```
ssh -Y -l <username> comet.sdsc.edu
```

## Create a test directory
Clone one of these repositories or use one you have already created
* [SDSC HPC Notebook Examples](https://github.com/sdsc-hpc-training-org/notebook-examples)
```
git clone https://github.com/sdsc-hpc-training-org/notebook-examples.git
```

* [Bob Sinkovit's Python Series](https://github.com/sinkovit/PythonSeries)
```
git clone git@github.com:sinkovit/PythonSeries.git
```
## Launch the secure notebook Using the *Reverse Proxy Service*
```
start-notebook
```
For more information on using ```start-notebook``` including configuration and installation, see https://comet-notebooks-101.readthedocs.io/en/comet/methods/reverseProxy.html

## NOTE: The instructions below are for running *INSECURE* notebooks over HTTP (not HTTPS).
This method is not supported or recommended by SDSC. Your notebooks will run over HTTP, and be vulnerable to explotation

### Obtain an interactive node:
For more help see the [Interactive Computing Guide](https://github.com/sdsc-hpc-training-org/basic_skills/tree/master/interactive_computing)

```
srun --pty --nodes=1 --ntasks-per-node=24 -p debug -t 00:30:00 --wait 0 /bin/bash
srun: job 24000544 queued and waiting for resources
srun: job 24000544 has been allocated resources
[mthomas@comet-18-29:~/hpctrain/python/PythonSeries] 
```
Wait for your node to be allocated.
Load the  modules that know  about jupyter notebooks.
```
module load XXXXX
```
Check out the Readme.md files, it will explaing what is in the different notebooks.

Launch the Jupyter Notebook application. 
Note: this application will be running on comet, and you will be given a URL which will connect your local web browser the interactive comet session:
```
jupyter notebook --no-browser --ip=`/bin/hostname`
```
This will give you an address which has localhost in it and a token. Something
like:
```
http://comet-14-0-4:8888/?token=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
You can then paste it into your browser. You will see a running Jupyter
notebook and a listing of the notebooks in your directory. From there everything should be working as a regular notebook.

Notes:
1. This notebook is hosted over HTTP, which is INSECURE, for a secure notebook use the [Reverse Proxy Service](https://comet-notebooks-101.readthedocs.io/en/comet/methods/reverseProxy.html)
2. This token is your auth so don't email/send it around. It will go away when you stop the notebook. 
3. To learn about Python, see the tutorials [here](https://github.com/sdsc-hpc-training-org/notebook-examples/tree/master/Boring_Python) and [here](https://github.com/sinkovit/PythonSeries).
4. To see an example of remote visualization, run the  ```Matplotlib.ipynb```  notebook from the Sinkovits collection.



