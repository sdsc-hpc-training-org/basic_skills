# Using Jupyter Notebooks on the SDSC Expanse Cluster

### Overview

This quick-start guide will show you how to run [Jupyter notebooks on Expanse](https://hpc-training.sdsc.edu/notebooks-101/notebook-101.html) using the [Satellite Reverse Proxy Service](https://github.com/sdsc-hpc-training-org/satellite).

Satellite is a prototype system that allows users to launch secure (**HTTPS**) Jupyter services on Expanse compute nodes using a simple bash script such as **`galyleo`** or **`start_notebook`**. The notebooks are made available outside the cluster firewall using a *secure* HTTPS connection between your web browser and the reverse proxy server.

---

## Contents <a name="top"></a>

- [Using the galyleo script](#galyleo) — Launch secure Jupyter notebooks on Expanse  
- [Running CONDA Environments](#conda) — Use CONDA environments with Jupyter  
- [Notebook Examples](#ntbk-ex) — Example notebooks and repositories


---

## Using the galyleo script <a name="galyleo"></a>

[galyleo](https://github.com/mkandes/galyleo) is a shell utility that helps you launch Jupyter notebooks on high-performance computing (HPC) systems in a simple and secure way.

It works with the [Satellite reverse proxy service](https://github.com/sdsc-hpc-training-org/satellite) and a batch job scheduler such as Slurm to provide each Jupyter notebook server with its own **one-time, token-authenticated HTTPS connection** between the compute node and your web browser.

This HTTPS-secured connection provides privacy and integrity for the data exchanged between the notebook server and your browser, helping protect your work against network eavesdropping and data tampering.

:::note
For full usage details, see the galyleo repository:  
https://github.com/mkandes/galyleo
:::

---

## Running CONDA Environments and Jupyter Notebook on Expanse <a name="conda"></a>

For a detailed walkthrough on using CONDA environments with Jupyter on Expanse, see the CIML Summer Institute material:

- [Session 3.3 — CONDA Environments and Jupyter Notebook on Expanse: Scalable & Reproducible Data Exploration and ML](https://github.com/ciml-org/ciml-summer-institute-2023/tree/main/3.3_conda_environments_and_jupyter_notebook_on_expanse)

---

## Example Notebooks <a name="ntbk-ex"></a>

Clone the notebook example repository, or use one you have already created:

- [SDSC HPC Notebook Examples](https://github.com/sdsc-hpc-training-org/notebook-examples-expanse)

```bash
git clone https://github.com/sdsc-hpc-training-org/notebook-examples-expanse.git
```

Once cloned, you can launch a secure notebook using the **galyleo** command.

---

_Last updated: April 24, 2024_  
_Author: [Mary Thomas, SDSC](https://www.sdsc.edu/research/researcher_spotlight/thomas_mary.html)_

[Back to Top](#top)
