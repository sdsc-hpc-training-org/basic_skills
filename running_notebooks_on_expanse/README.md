# Using Jupyter Notebooks on the SDSC Expanse Cluster
**By** [Mary Thomas, SDSC](https://www.sdsc.edu/research/researcher_spotlight/thomas_mary.html)

**Updated:**  April 24, 2024

## [Contents](#top)
* [Using the galyleo script](#galyleo)
* [Running CONDA Environments and Jupyter Notebook on Expanse](#conda)
* [Notebook Examples](#ntbk-ex)

This quick-start guide will show you how to run [Jupyter notebooks on Expanse](https://hpc-training.sdsc.edu/notebooks-101/notebook-101.html) using the [Satellite Reverse Proxy Service](https://github.com/sdsc-hpc-training-org/satellite). Satellite is a prototype system that will allow users to launch secure (HTTPS) Jupyter Services on any Expanse compute node using a simple bash script called *galyleo* or *start_notebook*. The notebooks will be made available to the user outside of the cluster firewall using a *secure* HTTPS connection between the external users web browser and the reverse proxy server.

_______
## Using the galyleo script <a name="galyleo">
[galyleo](https://github.com/mkandes/galyleo) is a shell utility to help you launch Jupyter notebooks on high-performance computing (HPC) systems in a simple, secure way. It works with the [Satellite reverse proxy service](https://github.com/sdsc-hpc-training-org/satellite) and a batch job scheduler like Slurm to provide each Jupyter notebook server you start with its own one-time, token-authenticated HTTPS connection between the compute resources of the HPC system the notebook server is running on and your web browser. This HTTPS-secured connection affords both privacy and integrity to the data exchanged between the notebook server and your browser, helping protect you and your work against network eavesdropping and data tampering.

For details on using ```galyleo,``` see:  https://github.com/mkandes/galyleo

_______
### Running CONDA Environments and Jupyter Notebook on Expanse<a name="conda">
* see the CIML Summer Institute material: [Session 3.3 CONDA Environments and Jupyter Notebook on Expanse: Scalable & Reproducible Data Exploration and ML](https://github.com/ciml-org/ciml-summer-institute-2023/tree/main/3.3_conda_environments_and_jupyter_notebook_on_expanse)
______


###  Example Notebooks<a name="ntbk-ex">
Clone the notebook example repository, or use one you have already created
* [SDSC HPC Notebook Examples](https://github.com/sdsc-hpc-training-org/notebook-examples-expanse)
```
git clone https://github.com/sdsc-hpc-training-org/notebook-examples-expanse.git
```

* Launch the secure notebook Using the Galyleo command


