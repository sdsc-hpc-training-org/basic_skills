---
title: "Basic Environment"
sidebar_position: 1
---

### Basic system information

Using Unix commands, we can learn a lot about the machine we are logged onto. Some of the commands are simple:

```sh
[username@login02 ~]$ date
Tue Jan 16 20:20:23 PST 2024
[username@login02 ~]$ hostname
login02
[username@login02 ~]$ whoami
username
```

:::note
To learn about most unix commands, try accessing the `man` pages.
:::

```sh
[username@login02 ~]$ man date

NAME
       date - print or set the system date and time

SYNOPSIS
       date [OPTION]... [+FORMAT]
       date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]

DESCRIPTION
       Display the current time in the given FORMAT, or set the system date.
       ..... more info .....
```

---

### Environment variables

The unix command `env` will print out the _environment_ settings for your login session.  
The list below is an edited summary of all the information

:::warning
The output can be very long (over 90 lines)
:::

```sh
[username@login02 ~]$ env
MODULEPATH=/opt/modulefiles/mpi/.intel:/opt/modulefiles/applications/.intel:/opt/modulefiles/mpi:/opt/modulefiles/compilers:/opt/modulefiles/applications:/usr/share/Modules/modulefiles:/etc/modulefiles
LOADEDMODULES=intel/2013_sp1.2.144:mvapich2_ib/2.1:gnutools/2.69
HOME=/home/username
SDSCHOME=/opt/sdsc
LOGNAME=username
SSH_CONNECTION=xxx.xxx.xx.xx 53640 198.202.113.253 22
DISPLAY=localhost:48.0
```

---

### Printing environment variables

It is often useful to print out (or use) environment variables. To print them out, use the `echo` command, and `$` sign (which extracts the value of the shell variable):

```sh
[username@login02 ~]$ echo $SHELL
/bin/bash
[username@login02 ~]$ echo $HOME
/home/username
```

---

### Home directory shortcut

Another important environment variable is the home directory variable, the "tilde" character: `~`

```sh
[username@login02 ~]$ echo ~
/home/username
[username@login02 ~]$
```

---

### Creating environment variables

You can create your own environment variables:

```sh
[username@login02 ~]$ MY_NAME="Super User"
[username@login02 ~]$ echo $MY_NAME
Super User
```

---

### Users and groups

Unix has the concept of users and groups. Groups are used to control access to resources (files, applications, etc.) and help establish a secure envionment Users can be in more than one group. To see which groups you are a member of, use the `group` command:

```sh
[username@login02 OPENMP]$ groups
abc123 pet heart scicom-docs grdclus webwrt scwpf ...
```

---

[Back to Top](#top)
