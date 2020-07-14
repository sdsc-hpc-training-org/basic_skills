# Using Jupyter Notebooks on the SDSC Comet Cluster
**By** [Mary Thomas, SDSC](https://www.sdsc.edu/research/researcher_spotlight/thomas_mary.html)

This quick-start guide will show you how to run/edit a jupyter notebooks, from the command link. 

## Installing and Setting up Jupyter Notebooks on Comet

See the full instructions and tutorials here:  [Running Notebooks on Comet](https://comet-notebooks-101.readthedocs.io/en/comet/index.html)


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

## Obtain an interactive node:
For more help see the [Interactive Computing Guide](https://github.com/sdsc-hpc-training-org/basic_skills/tree/master/interactive_computing)

```
srun --pty --nodes=1 --ntasks-per-node=24 -p compute -t 02:00:00 --wait 0 /bin/bash
srun: job 24000544 queued and waiting for resources
srun: job 24000544 has been allocated resources
[mthomas@comet-18-29:~/hpctrain/python/PythonSeries] 
```
Wait for your node to be allocated.
Load the singularity module that knows about jupyter notebooks and get an interactive shell
```
module load singularity
singularity shell /share/apps/gpu/singularity/sdsc_ubuntu_tf1.1_keras_R.img
```
Check out the Readme.md file, it will explaing what is in the different notebooks.
Launch the Jupyter Notebook application. 
Note: this application will be running on comet, and you will be given a URL which will connect your local web browser the interactive comet session:
```
ipython notebook --no-browser --ip=`/bin/hostname`
```
This will give you an address which has localhost in it and a token. Something
like:
```
http://comet-14-0-4:8888/?token=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
You can then paste it into your browser. You will see a running Jupyter
notebook and a listing of the notebooks in your directory. From there everything should be working as a regular notebook.
Note: This token is your auth so don't email/send it around. It will go away when you stop the notebook. 

To learn about Python, run the ```Python basics.ipynb```   notebook.
To see an example of remote visualization, run the  ```Matplotlib.ipynb```  notebook!



