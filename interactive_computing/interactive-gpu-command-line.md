---
title: "Obtain interactive shared GPU node on SDSC Expanse"
sidebar_position: 3
---

* This works the same way, but you need to access the GPU nodes.
* The SLURM launch command below will obtain an interactive node with access to **1 K80 GPU** on the shared GPU nodes for **3 hours**. You can also execute this command directly on the command line:

```bash
srun --partition=gpu-shared --reservation=gputraining --nodes=1 --ntasks-per-node=6 --gres=gpu:k80:1 -t 03:00:00 --pty --wait=0 /bin/bash
```

:::note
It may take some time to get the interactive node, depending on system availability.
:::

---

### Load required modules

Load the CUDA and PGI compiler modules:

```bash
module purge
module load gnutools
module load cuda
module load pgi
```

---

### Resolve PGI license errors (if needed)

If you get a license error when executing the PGI compilers, execute the following:

```bash
export LM_LICENSE_FILE=40200@elprado.sdsc.edu:$LM_LICENSE_FILE
```

---

[Back to Top](#top)
