---
title: "Request an interactive CPU node from the command line"
sidebar_position: 2
---

* You can request an interactive session using the The SLURM launch `srun` command.
* The following example will request one regular compute node, 4 cores, in the debug partition for 30 minutes.

```bash
srun --partition=debug --pty --account=<<project>> --nodes=1 --ntasks-per-node=4 --mem=8G -t 00:30:00 --wait=0 --export=ALL /bin/bash
```

* Wait for your node to be allocated.
* This may take a while, depending on how busy the system is.
* When you have your node, you will get a message like this:

```bash
srun: job 13469789 queued and waiting for resources
srun: job 13469789 has been allocated resources
[user@exp-9-55 ~]$
```

:::note
Notice that you are logged onto a different node than the login node.
:::

---

### Explore the compute node

Run some commands to learn about the node:

```bash
[user@exp-9-55 ~]$ hostname
exp-9-55.sdsc.edu
[user@exp-9-55 ~]$ who
[user@exp-9-55 ~]$ whoami
user
```

```bash
[user@exp-9-55 ~]$ top
top - 21:37:07 up 15 days, 15:58,  0 users,  load average: 0.03, 0.06, 0.05
Tasks: 620 total,   1 running, 619 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni, 99.9 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem : 13165400+total, 12897894+free,  1933784 used,   741272 buff/cache
KiB Swap:        0 total,        0 free,        0 used. 12866142+avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
17259 root      20   0   22408  15684   2476 S   0.7  0.0  30:25.44 serf
 6380 root      20   0       0      0      0 S   0.3  0.0   0:13.09 jbd2/md1-8
    1 root      20   0  192860   4816   1604 S   0.0  0.0   2:30.00 systemd
```

---

### Next steps

* At this point, you can edit, compile, and run code, including MPI, OpenMP, or Jupyter notebooks.
* For an example of running a notebook, see the following tutorial:
  * https://github.com/sdsc-hpc-training/basic_skills/tree/master/how_to_run_notebooks_on_expanse
* For a collection of test notebooks, see:
  * https://github.com/sdsc-hpc-training-org/notebook-examples-expanse

---

[Back to Top](#top)
