# Connecting to SDSC HPC Resources: Accounts and Connecting
In these tutorials, you will use your SDSC or XSEDE account to log onto the and SDSC cluster. These exercises verify that your accounts are working, that your laptop is properly configured, and that your Comet user environment is correctly setup.

SDSC HPC systems support *Single Sign On (SSO)* through the *XSEDE User Portal* and from the command line using an XSEDE-wide password. To log in to Comet from the command line, use the hostname:

comet.sdsc.edu 
The following are examples of Secure Shell (ssh) commands that may be used to log in to Comet:

ssh <your_username>@comet.sdsc.edu
ssh -l <your_username> comet.sdsc.edu 
Notes and hints
When you log in to comet.sdsc.edu, you will be assigned one of the four login nodes comet-ln[1-4].sdsc.edu. These nodes are identical in both architecture and software environment. Users should normally log in through comet.sdsc.edu, but may specify one of the four nodes directly if they see poor performance.
Please feel free to append your public RSA key to your ~/.ssh/authorized_keys file to enable access from authorized hosts without having to enter your password. Make sure you have a password on the private key on your local machine. You can use ssh-agent or keychain to avoid repeatedly typing the private key password.
Do not use the login nodes for computationally intensive processes.  These nodes are meant for compilation, file editing, simple data analysis, and other tasks that use minimal compute resources. All computationally demanding jobs should be submitted and run through the batch queuing system.
## Updated   July 2020

* [Connecting to Comet](https://github.com/sdsc-hpc-training-org/basic_skills/blob/master/connecting-to-hpc-systems/connect-to-comet.md)


