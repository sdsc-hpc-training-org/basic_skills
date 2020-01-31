# Connecting to your Comet.sdsc.edu Account
[//]: # " Comment example "

[//]: # ( Comment2 )

In this exercise, you must use your SDSC or XSEDE account to log onto the Comet cluster. This exercise verifies that your account is working, that your laptop is properly configured, and that your Comet user environment is correctly setup.

<a name="top">In this document, we will show you how to:
    
* [Obtain your Comet account](#obtain-your-comet-account)
* [Using the Terminal Application to connect to Comet](#term-app)
    - [Mac Users](#term-app-mac-users)
    - [Windows Users](#term-app-windows)
        - [Windows 10](#term-app-windows10)
        - [Windows (pre-Win10)](#term-app-windows-older)
    - [Terminal Connection Example](#term-app-example)
    - [Getting Domain Name & Host Information](#term-app-dn-info)
* [Connect via Passwordless SSH](#passwordless)

Note: if you have any difficulties completing this task, please contact Institute staff at <consult@sdsc.edu>.

### Please read the Comet user guide and familiarize yourself with the hardware, file systems, batch job submission, compilers and modules.

Comet User Guide: http://www.sdsc.edu/support/user_guides/comet.html
 

## <a name="obtain-your-comet-account"></a>Obtain your comet account:

To obtain a trial Comet account see the Comet user guids at  http://www.sdsc.edu/support/user_guides/comet.html#trial_accounts

[Back to Top](#top)
<hr>

## <a name="term-app"></a>How to Use the Terminal Application:

The terminal applications are used to connect clients (you and your laptop) to remote computers (such as Comet). See https://en.wikipedia.org/wiki/Secure_Shell for more information. The best known example of using a terminal is for logging in/connecting to a remote computer systems by users. This is called a client-server connection. Terminals are interactive: you type in a command to run, and the outputs are displayed on the terminal. Executing any command is done by typing it and pressing Enter.

<img src="./images/ssh-login-comet.png" alt="SSH Connection" width="300px" />

SSH provides a secure channel over any network in a client-server architecture. You will be using your laptop to access SDSC’s HPC systems using the secure shell command `ssh`. It is essential that you be able to run secure shell (or a similar connection tool) with X11 forwarding enabled, which allows you to have data encryption and to launch windows applications (e.g. plotting, or a browser).

*NOTE: The `hostname` for Comet is `comet.sdsc.edu`

<img src="./images/cluster-connection-diagram.png" alt="SSH Connection" width="350px" />

[Back to Top](#top)
<hr>

## <a name="term-app-mac-users"></a>Mac Users
For Mac users, the Terminal application is typically used for connections. This is done from the command line:

    ssh -X username@<hostname>

 If you are having trouble, try running `ssh` in verbose mode:

     ssh -v -X username@hostname


[Back to Top](#top)
<hr>

## <a name="term-app-windows"></a>MSFT Windows 
All windows users will need to run a terminal emulation application capable of supporting an X Server and an ssh-like client.

### <a name="term-app-windows10"></a>Windows 10
Windows Terminal is a terminal emulator for Windows 10 written by Microsoft. It includes support for the Command Prompt, PowerShell, WSL and SSH. The terminal emulator is described here: https://en.wikipedia.org/wiki/Windows_Terminal.

<img src="./images/windows-10-powershell-commands.png" alt="Win10 Powershell" width="350px" />

To download and install the PowerShell application, see here [ Available Jan 30, 2020: ] : https://docs.microsoft.com/en-us/skypeforbusiness/set-up-your-computer-for-windows-powershell/download-and-install-windows-powershell-5-1

[Back to Top](#top)
<hr>

### <a name="term-app-windows-older"></a> Windows (pre-Win10)
Older  [Cygwin](https://www.cygwin.com) provides a comprehensive Linux-like environment and an X server (Cygwin/X). Putty will also work for direct access to Comet, it is only used for file transfers. For download and installation instructions, see:

* http://www.cygwin.com/
* http://x.cygwin.com/
* https://www.putty.org/

[Back to Top](#top)
<hr>

## <a name="term-app-example"></a>Example of a terminal connection:
```
Rocks 7.0 (Manzanita)
Profile built 12:32 03-Dec-2019

Kickstarted 13:47 03-Dec-2019
                                                                       
                      WELCOME TO 
      __________________  __  _______________
        -----/ ____/ __ \/  |/  / ____/_  __/
          --/ /   / / / / /|_/ / __/   / /
           / /___/ /_/ / /  / / /___  / /
           \____/\____/_/  /_/_____/ /_/

```

[Back to Top](#top)
<hr>

## <a name="term-app-dn-info"></a>Getting Domain Name & Host Information
Each machine you work with will have a `<domain_name>`,  `<hostname>` or `<ip_address>`. You can learn about IP addresses and domain names here: https://computer.howstuffworks.com/dns.htm.

* NOTE: The *DN* (domain name) for Comet is    `comet.sdsc.edu`

You may need to know the physical IP address of the cluster. To do this, run the `nslookup` command from the command line of your terminal window
```
[username@comet:] nslookup comet.sdsc.edu
Server:		192.168.86.1
Address:	192.168.86.1#53

Non-authoritative answer:
Name:	comet.sdsc.edu
Address: 198.202.113.253
Name:	comet.sdsc.edu
Address: 198.202.113.252
```

The IP address is the  line labeled "Address" and for Comet there are two. YOu can log onto Comet using either the DN or the IP addresses.

[Back to Top](#top)

<hr>

## <a name="passwordless"></a>Connect via Passwordless SSH

To configure your login using *passwordless ssh*, see this tutorial:
* https://www.tecmint.com/ssh-passwordless-login-using-ssh-keygen-in-5-easy-steps

