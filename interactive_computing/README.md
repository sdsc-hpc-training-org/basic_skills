# Interactive Computing on the Expanse Cluster
Interactive HPC systems allow real-time user inputs in order to facilitate code development, real-time data exploration, and visualizations. An interactive job (also referred as interactive session) will provide you with a shell on a compute node in which you can launch your jobs. In this tutorial we show you how to obtain interactive nodes on SDSC HPC systems

**Note** For more details on using Expanse, see the user guide: https://www.sdsc.edu/support/user_guides/expanse.html

<!-- TOC -->
<a name="top">Contents
* [Obtaining Interactive Nodes](#interactive-nodes)
  * [Log onto expanse.sdsc.edu](#log-onto-expanse)
  * [Request an interactive node from the command line:](#interactive-node-command-line)
* [Obtain interactive shared GPU node on Expanse](#interactive-gpu-command-line)

<!-- tocstop -->


## Obtaining Interactive Nodes<a name="interactive-nodes"></a>
There are two ways to obtain interactive nodes: 
1. via the command line
2. via a batch script

### First, Log onto expanse.sdsc.edu  <a name="X"></a>
```
ssh -Y -l <username> expanse.sdsc.edu
```

* To learn more about logging onto the Expase cluster, see these instructions: https://github.com/sdsc-hpc-training-org/hpc-security/blob/master/connecting-to-hpc-systems/connect-to-expanse.md
 
[Back to Top](#top)
<hr>
 
### Request an interactive node from the command line:  <a name="interactive-node-command-line"></a>
 * You can request an interactive session using the srun command. The following example will request one regular compute node, 4 cores,  in the debug partition for 30 minutes.

```
srun --partition=debug --qos=debug-normal --pty   --nodes=1 --ntasks-per-node=128 --mem=248 -t 00:30:00 --wait=0 --export=ALL --account=<<ACCT>> /bin/bash
```

* Wait for your node to be allocated.
* This may take a long time, depending on how busy the system is.
* When you have your node, you will get a message like this:

 ```
srun: job 13469789 queued and waiting for resources
srun: job 13469789 has been allocated resources
[user@exp-9-55 ~]$  
 ```
 
*Notice that you are logged onto a different node than the login node.
* Run some commands to learn about the node:

 ```
[user@exp-9-55 ~]$   hostname
exp-9-55.sdsc.edu
[user@exp-9-55 ~]$  who
[user@exp-9-55 ~]$  whoami
user
[user@exp-9-55 ~]$ 
[user@exp-9-55 ~]$  
top - 21:37:07 up 15 days, 15:58,  0 users,  load average: 0.03, 0.06, 0.05
Tasks: 620 total,   1 running, 619 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni, 99.9 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem : 13165400+total, 12897894+free,  1933784 used,   741272 buff/cache
KiB Swap:        0 total,        0 free,        0 used. 12866142+avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND                              
17259 root      20   0   22408  15684   2476 S   0.7  0.0  30:25.44 serf                                 
 6380 root      20   0       0      0      0 S   0.3  0.0   0:13.09 jbd2/md1-8                           
    1 root      20   0  192860   4816   1604 S   0.0  0.0   2:30.00 systemd                              
    2 root      20   0       0      0      0 S   0.0  0.0   0:02.72 kthreadd                             
    3 root      20   0       0      0      0 S   0.0  0.0   0:07.61 ksoftirqd/0                          
    8 root      rt   0       0      0      0 S   0.0  0.0   0:01.05 migration/0                          
    9 root      20   0       0      0      0 S   0.0  0.0   0:00.00 rcu_bh                               
   10 root      20   0       0      0      0 S   0.0  0.0   4:00.35 rcu_sched       
```
At this point, you can edit, compile, run code, including MPI, OpenMP, or jupyter notebooks.
For an example of running a notebook, see the __How to Run Notebooks on Expanse__ tutorial:
https://github.com/sdsc-hpc-training/basic_skills/tree/master/how_to_run_notebooks_on_expanse

[Back to Top](#top)
<hr>
 
## Obtain interactive shared GPU node on SDSC Expanse <a name="interactive-gpu-command-line"></a>
This works the same way, but you need to access the GPU nodes

The command below will launch the command ```srun```

```
srun -t 00:30:00 --partition=gpu-shared --nodes=1 --ntasks-per-node=7 \
     --gres=gpu:p100:1 --reservation=sccgpures --pty --wait=0 /bin/bash
```

The SLURM launch command below to obtain an interactive node with access to 1 K80 GPU on the shared GPU nodes for 3h. You can also execute this command directly on the command line:
```
srun --partition=gpu-shared --reservation=gputraining \
     --nodes=1 --ntasks-per-node=6 --gres=gpu:k80:1 \
     -t 03:00:00 --pty --wait=0 /bin/bash
```
It may take some time to get the interactive node.

Load the CUDA and PGI compiler modules
```
module purge
module load gnutools
module load cuda
module load pgi
```
If you get a license error when executing the PGI compilers, execute the following:

```
export LM_LICENSE_FILE=40200@elprado.sdsc.edu:$LM_LICENSE_FILE
```
[Back to Top](#top)
<hr>
