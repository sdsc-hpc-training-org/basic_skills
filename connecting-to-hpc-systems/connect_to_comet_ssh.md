# Preparing to Work on SDSC HPC Resources: Accounts and Connecting


[//]: # " Comment example "

[//]: # ( Comment2 )

In this exercise, you must use your SDSC or XSEDE account to log onto the Comet cluster. To do this you need a comet account, and an application that can be used to connect to Comet using [SSH](https://en.wikipedia.org/wiki/Secure_Shell). This exercise verifies that your account is working, that your laptop is properly configured, and that your Comet user environment is correctly setup.

<a name="top">In this document, we will show you how to:
    
* [Obtain your Comet account](#obtain-your-comet-account)
* [Getting Domain Name & Host Information](#term-app-dn-info)
* [Using a Terminal Application to Connect to Comet](#term-app)
    - [Mac Users](#term-app-mac-users)
    - [Windows Users](#term-app-windows-users)
    - [Terminal Connection Example](#term-app-example)
* [Expand your knowledge using Comet User guide](#comet-user-guide)

Note: if you have any difficulties completing this task, please contact HPC consulting at <consult@sdsc.edu>.

## <a name="obtain-your-comet-account"></a>Obtain your comet account:

To obtain a trial Comet account see the Comet user guide at  http://www.sdsc.edu/support/user_guides/comet.html#trial_accounts

You will be directed to the XSEDE portal, where you will create a Portal User account. Information from that account will be used to set up your *trial* Comet account. Note that the Portal account and the Comet account may be different, so keep track of them both. The Comet account can then be used for other Comet allocations.

[Back to Top](#top)
<hr>

## <a name="term-app-dn-info"></a>Getting Domain Name & Host Information
Each machine you work with will have a `<domain_name>`,  `<hostname>` or `<ip_address>`. You can learn about IP addresses and domain names here: https://computer.howstuffworks.com/dns.htm.

* NOTE: The *DN* (domain name) for Comet is    `comet.sdsc.edu`

You may need to know the physical IP address of the cluster. To do this, run the `nslookup` command from the command line of your local terminal window (or on comet if are logged in)
```
[username@laptop:] nslookup comet.sdsc.edu
Server:		192.168.86.1
Address:	192.168.86.1#53

Non-authoritative answer:
Name:	comet.sdsc.edu
Address: 198.202.113.252
Name:	comet.sdsc.edu
Address: 198.202.113.253
```

The public IP address appears under the line labeled "Non-authoritative answer:" and for Comet there are two. * Comet's DN is. comet.sdsc.edu
* Comet's IP address is 198.202.113.252 and 198.202.113.253. 
* You can log onto Comet using either the DN or the IP addresses. 

[Back to Top](#top)
<hr>

## <a name="term-app"></a>Using a Terminal Application to Connect to Comet:

The terminal applications are used to connect clients (you and your laptop) to remote computers (such as Comet). See https://en.wikipedia.org/wiki/Secure_Shell for more information. The best known example of using a terminal is for logging in/connecting to a remote computer systems by users. This is called a client-server connection. Terminals are interactive: you type in a command to run, and the outputs are displayed on the terminal. Executing any command is done by typing it and pressing Enter.

<img src="ssh-login-comet.png" alt="SSH Connection" width="300px" />

SSH provides a secure channel over any network in a client-server architecture. You will be using your laptop to access SDSC’s HPC systems using the secure shell command `ssh`. It is essential that you be able to run secure shell (or a similar connection tool) with X11 forwarding enabled, which allows you to have data encryption and to launch windows applications (e.g. plotting, or a browser).

*NOTE: The `hostname` or `DN` for Comet is `comet.sdsc.edu`

<img src="cluster-connection-diagram.png" alt="SSH Connection" width="350px" />

[Back to Top](#top)
<hr>

## <a name="term-app-mac-users"></a>Mac Users
For Mac users, the Terminal application is typically used for connections. This is done from the command line:

    ssh -X username@<hostname>

 If you are having trouble, try running `ssh` in verbose mode:

     ssh -v -X username@hostname

To configure your login using *passwordless ssh*, see this tutorial:

https://www.tecmint.com/ssh-passwordless-login-using-ssh-keygen-in-5-easy-steps/

[Back to Top](#top)
<hr>

## <a name="term-app-windows-users"></a>Windows users
* **Windows 10** has a new terminal app called *Windows Terminal*, which is a terminal emulator for Windows 10 written by Microsoft. It includes support for the Command Prompt, PowerShell, WSL and SSH and other commands. While not a full Unix OS, it has shown to be very popular and useful within the HPC community. MSFT has created a GitHub repo with source code, installation and documentation here:
   * https://github.com/Microsoft/Terminal

* **Older Windows** users will need to run an X Server and an ssh-like client. [Cygwin](https://www.cygwin.com) provides a comprehensive Linux-like environment and an X server (Cygwin/X). Putty will also work for direct access to Comet, it is only used for file transfers. For download and installation instructions, see:

   * http://www.cygwin.com/
   * http://x.cygwin.com/
   * https://www.putty.org/

[Back to Top](#top)
<hr>

## <a name="term-app-example"></a>Example of a terminal connection:
```
[localuser@localhost]: ssh -X username@comet.sdsc.edu
Last login: Wed Apr 15 09:58:45 2020 from 12.345.67.89
Rocks 7.0 (Manzanita)
Profile built 12:32 03-Dec-2019

Kickstarted 13:47 03-Dec-2019
                                                                       
                      WELCOME TO 
      __________________  __  _______________
        -----/ ____/ __ \/  |/  / ____/_  __/
          --/ /   / / / / /|_/ / __/   / /
           / /___/ /_/ / /  / / /___  / /
           \____/\____/_/  /_/_____/ /_/
###############################################################################
NOTICE:
The Comet login nodes are not to be used for running processing tasks.
This includes running Jupyter notebooks and the like.  All processing
jobs should be submitted as jobs to the batch scheduler.  If you don’t
know how to do that see the Comet user guide
https://www.sdsc.edu/support/user_guides/comet.html#running.
Any tasks found running on the login nodes in violation of this policy
 may be terminated immediately and the responsible user locked out of
the system until they contact user services.
###############################################################################
[username@comet-ln2 ~]$
```
Now that you are logged onto Comet, you can begin working with your code. If you are new to Unix, please see the tutorials:
* [Basic Linux Skills](https://github.com/sdsc-hpc-training/webinars/tree/master/basic_skills/basic_linux_skills)
* [Comet 101](https://github.com/sdsc-hpc-training/webinars/tree/master/20200416_comet_101)


[Back to Top](#top)
<hr>


## <a name="comet-user-guide"></a>Comet User Guide

Please read the Comet user guide and familiarize yourself with the hardware, file systems, batch job submission, compilers and modules. The guide can be found here:

http://www.sdsc.edu/support/user_guides/comet.html
