# Using Jupyter Notebooks on the SDSC Comet Cluster
**By** [Mary Thomas, SDSC](https://hpc-students.sdsc.edu/instr_bios/mary_thomas.html)

## This tutorial will show you how to run/edit a jupyter notebooks, from the command link.
* Log onto comet.sdsc.edu  
```
ssh -Y -l <username> comet.sdsc.edu
```

* create a test directory, or ```cd``` into one you have already created
* Clone this repository (developed by Bob Sinkovits):   [https://github.com/sinkovit/PythonSeries](https://github.com/sinkovit/PythonSeries)
```
git clone git@github.com:sinkovit/PythonSeries.git
```

Get an interactive node:
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



