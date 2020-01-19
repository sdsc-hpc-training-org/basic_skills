# Accessing HPC Systems:  Basic Linux Skills
[//]: # " Comment example "

[//]: # ( Comment2 )

When you log on to Comet, your computer operating system will be a Unix shell. \"_A Unix shell is a command-line interpreter or shell that provides a traditional Unix-like command line user interface. This environment is very different from the easy to use GUI interfaces we have all become used in the Windows and MacOS systems_\" (https://en.wikipedia.org/wiki/Unix_shell).

Basic Linux skills are necessary to complete the hands-on exercises. If it’s been a while since you’ve worked in a Linux environment, be sure to reacquaint yourself with the following topic (many of which are demonstrated below)s: copying, listing, deleting and renaming files; using wildcards; navigating directories; changing file permissions; setting environment variables; using common utilities (grep, cat, less, head, sort, tar, gzip). A nice tutorial can be found here http://www.ee.surrey.ac.uk/Teaching/Unix/. You should also be comfortable with one of the standard Linux editors, such as vim, emacs, or nano.

You should also be comfortable with one of the standard Linux editors, such as vim, emacs, or nano.

Notes:
* For the examples below, we are using the `bash` shell, which is the default shell for new accounts on Comet. For the purposes of the Institute exercises, please do not change the shell.

<a name="top">**Examples::**
* [Basic Environment](#basic-env)
* [Directories and Navigation](#dirs-and-nav)
* [Files](#files)
* [Directories](#directories)
* [Permissions](#permissions)
* [Wildcards](#wildcards)
* [Common Utilities](#common-utilities)


Note: if you have difficulties completing this task, please contact Institute staff at <consult@sdsc.edu>.
<hr>

## <a name="basic-env">Basic Environment</a>
Using Unix commands, we can learn a lot about the machine we are logged onto. Some of the commands are simple:

```
[mthomas@comet-ln2 ~]$ date
Tue Jul 17 18:54:37 PDT 2018
[mthomas@comet-ln2 ~]$ hostname
comet-ln2.sdsc.edu
[mthomas@comet-ln2 ~]$ whoami
mthomas
```
Note: To learn about most unix commands, try accessing the `man` pages:
``` sh
[mthomas@comet-ln2 ~]$ man date

NAME
       date - print or set the system date and time

SYNOPSIS
       date [OPTION]... [+FORMAT]
       date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]

DESCRIPTION
       Display the current time in the given FORMAT, or set the system date.
       ..... more info .....
```

The unix command `env` will print out the _environment_ settings for your login session.
The list below is an edited summary of all the information
```
(base) [mthomas@comet-ln2:~] env
MKLROOT=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/mkl
MANPATH=/opt/intel/2018.1.163/documentation_2018/en/man/common:/usr/share/man:/usr/local/share/man
PDSHROOT=/opt/pdsh
XDG_SESSION_ID=11111609
HOSTNAME=comet-ln2.sdsc.edu
[snip lines]
CONDA_PREFIX=/home/mthomas/miniconda3
TBBROOT=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/tbb
PWD=/home/mthomas
_LMFILES_=/opt/modulefiles/compilers/intel/2018.1.163:/opt/modulefiles/mpi/mvapich2_ib/2.3.2
JAVA_HOME=/usr/java/latest
GDB_CROSS=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/bin/intel64/gdb-mic
LANG=en_US.UTF-8
MODULEPATH=/opt/modulefiles/mpi/.intel:/opt/modulefiles/mpi:/opt/modulefiles/compilers:/opt/modulefiles/applications:/usr/share/Modules/modulefiles:/etc/modulefiles
LOADEDMODULES=intel/2018.1.163:mvapich2_ib/2.3.2
JUPYTER_CONFIG_DIR=/home/mthomas/.jupyter
LM_LICENSE_FILE=/opt/flexlm/license/license.dat
_CE_M=
MPM_LAUNCHER=/opt/intel/2018.1.163/debugger_YEAR/mpm/intel64_igfx/bin/start_mpm.sh
HISTCONTROL=ignoredups
INTEL_PYTHONHOME=/opt/intel/2018.1.163/debugger_YEAR/gdb/intel64/share/gdb/python
SHLVL=1
HOME=/home/mthomas
ROLLSROOT=/opt/rocks/share/devel/src/roll
MPIHOME=/opt/mvapich2/intel/ib
[snip]
}
_=/bin/env
```
It is often useful to print out (or use) environment variables. To print them out, use the `echo` command, and `$` sign (which extracts the value of the shell variable):
```
[mthomas@comet-ln2 ~]$ echo $SHELL
/bin/bash
[mthomas@comet-ln2 ~]$ echo $HOME
/home/mthomas
```
Another important environment variable is the home directory variable, the \"tilde\" character:  `~`
```
[mthomas@comet-ln2 testdir]$ echo ~
/home/mthomas
[mthomas@comet-ln2 testdir]$
```
You can create your own environment variables:
```
[mthomas@comet-ln2 ~]$ MY_NAME="Mary Thomas"
[mthomas@comet-ln2 ~]$ echo $MY_NAME
Mary Thomas
```

Unix has the concept of users and groups. Users can be in more than one group. To see which groups you are a member of, use the `group` command:
```
[mthomas@comet-ln2 OPENMP]$ groups
use300 pet heart scicom-docs ...
```

[Back to Top](#top)
<hr>

## <a name="dirs-and-nav">Files, Directories and Navigation</a>
In unix, everything is a file, which can be confusing at first. The locations for where files are stored are also called directories (which is equivalent to folders). To find out where you are in the system, use the `pwd` command, which prints the full path to the current/working directory:
```
[mthomas@comet-ln2 ~]$ pwd
/home/mthomas
```
To see what are the contents of the directory, use the file listing command `ls`
```
[mthomas@comet-ln2 ~]$ ls
filelisting.txt intel   loadgccomgnuenv.sh  loadgnuenv.sh	loadintelenv.sh  tools
```
In every Unix directory, there are \"hidden\" files (just like on Macs and Windows machines), to see them, run the `ls -a` command:
```
[mthomas@comet-ln2 ~]$ ls -a
.	.bash_history  .bashrc	 .gitconfig  loadgccomgnuenv.sh  .ncviewrc     .ssh	 .vimrc
..	.bash_logout   .config filelisting.txt	 intel	     loadgnuenv.sh	 .petscconfig  tools	 .Xauthority
.alias	.bash_profile    .kshrc      loadintelenv.sh	 .slurm        .viminfo
```
In Unix, sometimes it is hard tell if a file is also a directory. To see file details (including timestamp and size), run the `ls -l` command:
```
[mthomas@comet-ln2 ~]$ ls -l
drwxr-xr-x  2 mthomas use300        4 Apr 10  2019 bigdatafiles
drwxr-xr-x  5 mthomas use300        7 Jan  7  2019 comet-examples
-rw-r--r--  1 mthomas use300   265000 Oct  9 17:52 comet.share.tree.txt
drwxr-xr-x  7 mthomas use300        7 Aug 20 09:27 cuda
[snip extra lines]
-rw-r--r-- 1 mthomas use300 1543 Jul 17 21:04 filelisting.txt
drwxr-xr-x 3 mthomas use300   3 Jun 22  2017 intel
-rwx------ 1 mthomas use300 101 Jun 27  2017 loadgccomgnuenv.sh
-rwx------ 1 mthomas use300  77 Oct 16  2017 loadgnuenv.sh
-rwxr-xr-x 1 mthomas use300 125 Oct 16  2017 loadintelenv.sh
drwxr-xr-x 2 mthomas use300   4 Jun 30  2017 tools
```
You can combine the two commands above and use it to see the full directory and file information:
```
[mthomas@comet-ln2 ~]$ ls -al
total 74296
drwxr-x---  47 mthomas use300       73 Jan 18 14:42 .
drwxr-xr-x 133 root    root          0 Jan 18 15:05 ..
-rw-r--r--   1 mthomas use300     1001 Jul 11  2019 .bash_aliases
-rw-------   1 mthomas use300    38292 Jan 18 15:04 .bash_history
-rw-r--r--   1 mthomas use300       18 Jun 19  2017 .bash_logout
-rw-r--r--   1 mthomas use300      214 Aug  5 01:07 .bash_profile
-rw-r--r--   1 mthomas use300     1193 Aug  5 01:11 .bashrc
drwxr-xr-x   2 mthomas use300        4 Apr 10  2019 bigdatafiles
drwxr-xr-x   4 mthomas use300        4 Nov 13 13:32 .cache
drwxr-xr-x   5 mthomas use300        7 Jan  7  2019 comet-examples
-rw-r--r--   1 mthomas use300   265000 Oct  9 17:52 comet.share.tree.txt
[snip extra lines]
drwxr-xr-x   5 mthomas use300        5 Jun 12  2019 .ipython
drwxr-xr-x   3 mthomas use300        6 Nov  1 14:02 .jupyter
drwxr-xr-x   2 mthomas use300       29 Jan 16 14:25 jupyterhub-tst
-rw-r--r--   1 mthomas use300      550 Dec 10 15:01 jupyter_notebook_config.py
drwxr-xr-x   3 mthomas use300        5 Apr 23  2019 KANDES
drwxr-xr-x   2 mthomas use300        3 Jun 12  2019 .keras
-rw-r--r--   1 mthomas use300      171 Jun 19  2017 .kshrc
-rw-------   1 mthomas use300       62 Jul 31 12:46 .lesshst
-rwx------   1 mthomas use300      146 Apr 10  2019 loadgccomgnuenv.sh
-rwx------   1 mthomas use300      122 Apr 10  2019 loadgnuenv.sh
-rwx------   1 mthomas use300       96 Apr 10  2019 loadgpuenv.sh
-rwx------   1 mthomas use300      169 Apr 10  2019 loadintelenv.sh
-rwx------   1 mthomas use300      192 Apr 10  2019 loadRenv.sh
-rw-r--r--   1 mthomas use300      164 Jul 30 11:16 load.singularity.notebook.sh
drwx------   3 mthomas use300        3 Jun 12  2019 .local
drwxr-xr-x  57 mthomas use300       58 Jul 31 16:40 miniconda3
-rw-r--r--   1 mthomas use300 75257002 Jul 29 07:25 Miniconda3-latest-Linux-x86_64.sh
[snip extra lines]
```
There are several things to notice in the above listing: the first column of data is information about the file "permissions\", which controls who can see/read/modify what files (`r`=read, `w`=write,`x`=execute,`-`=no permission); the next 2 columns are the username and groupID; the 3rd and 4th columns are the size and date. This is discussed in more detail in the [Permissions](#permissions) section below. Also, note that two files have `dots` for their names: in unix the "dot" is a component of a filename. When working with filenames, a leading dot is the prefix of a "hidden" file, a file that an `ls` will not normally show. But also, the single dot, `.` represents the current working directory, and the double dots, `..` represent the directory above. You use these as arguments to unix commands dealing with directories.


To create directories, use the `mkdir`, make directory command:
```
[mthomas@comet-ln2 ~]$ mkdir testdir
(base) [mthomas@comet-ln2:~] ls -l testdir
total 84
drwxr-xr-x  2 mthomas use300    4 Jul 17  2018 .
drwxr-x--- 47 mthomas use300   73 Jan 18 14:42 ..
-rw-r--r--  1 mthomas use300 1543 Jul 17  2018 filelisting.txt
-rw-r--r--  1 mthomas use300    0 Jul 17  2018 newfile.txt
```
To move into that directory, use the `cd`, change directory command:
```
[mthomas@comet-ln2 ~]$ cd testdir/
[mthomas@comet-ln2 testdir]$ ls -al
total 20
drwxr-xr-x  2 mthomas use300    4 Jan 18 15:10 .
drwxr-x--- 47 mthomas use300   73 Jan 18 14:42 ..
[mthomas@comet-ln2 testdir]$
```
From this directory, you can use the `..` command to see the contents of the directory above:

```
[mthomas@comet-ln2 testdir]$ ls -l ..
total 74296
drwxr-x---  47 mthomas use300       73 Jan 18 14:42 .
drwxr-xr-x 131 root    root          0 Jan 18 15:05 ..
-rw-r--r--   1 mthomas use300     1001 Jul 11  2019 .bash_aliases
-rw-------   1 mthomas use300    38292 Jan 18 15:04 .bash_history
-rw-r--r--   1 mthomas use300       18 Jun 19  2017 .bash_logout
-rw-r--r--   1 mthomas use300      214 Aug  5 01:07 .bash_profile
-rw-r--r--   1 mthomas use300     1193 Aug  5 01:11 .bashrc
drwxr-xr-x   2 mthomas use300        4 Apr 10  2019 bigdatafiles
drwxr-xr-x   4 mthomas use300        4 Nov 13 13:32 .cache
drwxr-xr-x   5 mthomas use300        7 Jan  7  2019 comet-examples
-rw-r--r--   1 mthomas use300   265000 Oct  9 17:52 comet.share.tree.txt
[snip extra lines]
```

[Back to Top](#top)
<hr>


## <a name="wildcards">Wildcards</a>

\"A wildcard is a character that can be used as a substitute for any of a class of characters in a search, thereby greatly increasing the flexibility and efficiency of searches."  The wildcards are very powerful, and there is not room in this document for all of them, so we recommend that you check out this site:  http://www.linfo.org/wildcard.html for more information.

In the example below, we filter the file listing of _/dev_ with the use of the star wildcard to list all _tty_ files:

```

(base) [mthomas@comet-ln2:~/comet-examples/HPCT/MPI] ls /dev/*tty*
crw-rw-rw- 1 root tty     5,  0 Jan 18 16:54 /dev/tty
crw--w---- 1 root tty     4,  0 Dec  3 13:53 /dev/tty0
crw--w---- 1 root tty     4,  1 Dec  3 13:53 /dev/tty1
crw--w---- 1 root tty     4, 10 Dec  3 13:53 /dev/tty10
crw--w---- 1 root tty     4, 11 Dec  3 13:53 /dev/tty11
crw--w---- 1 root tty     4, 12 Dec  3 13:53 /dev/tty12
[snip lines]
crw--w---- 1 root tty     4,  8 Dec  3 13:53 /dev/tty8
crw--w---- 1 root tty     4,  9 Dec  3 13:53 /dev/tty9
crw-rw---- 1 root dialout 4, 64 Dec  3 13:53 /dev/ttyS0
crw-rw---- 1 root dialout 4, 65 Dec  3 13:53 /dev/ttyS1
crw-rw---- 1 root dialout 4, 66 Dec  3 13:53 /dev/ttyS2
crw-rw---- 1 root dialout 4, 67 Dec  3 13:53 /dev/ttyS3
```
You will see this command used often.


## <a name="files">Manipulating Files</a>

This section will show you how to manipulate files: copying, listing, deleting and renaming
Continuing with the `testdir` we created above, we can create files in many ways. One is to use the `touch` commmand, which will create a file with no contents:
```
[mthomas@comet-ln2 testdir]$ touch myfile1.txt
[mthomas@comet-ln2 testdir]$ touch myfile2.txt
[mthomas@comet-ln2 testdir]$ ls -l
total 85
drwxr-xr-x  2 mthomas use300    6 Jan 18 15:12 .
drwxr-x--- 47 mthomas use300   73 Jan 18 14:42 ..
-rw-r--r--  1 mthomas use300    0 Jan 18 15:12 myfile1.txt
-rw-r--r--  1 mthomas use300    0 Jan 18 15:12 myfile2.txt
```

To copy a file from another directory  to the current directory, use the full path. In this example, we will copy a file named  _filelisting.txt_ file from the directory above, using the `..` (\"dot-dot\") variable for the directory location:

```java
[mthomas@comet-ln2 testdir]$ cp ../filelisting.txt .
[mthomas@comet-ln2 testdir]$ ls -al
total 85
drwxr-xr-x  2 mthomas use300    6 Jan 18 15:12 .
drwxr-x--- 47 mthomas use300   73 Jan 18 14:42 ..
-rw-r--r--  1 mthomas use300 1543 Jul 17  2018 filelisting.txt
-rw-r--r--  1 mthomas use300    0 Jan 18 15:12 myfile1.txt
-rw-r--r--  1 mthomas use300    0 Jan 18 15:12 myfile2.txt
```

To rename a file, use the `mv` (move) command:

```
(base) [mthomas@comet-ln2:~/testdir] mv myfile2.txt newfile.txt
(base) [mthomas@comet-ln2:~/testdir] ls -al
total 85
drwxr-xr-x  2 mthomas use300    5 Jan 18 15:13 .
drwxr-x--- 47 mthomas use300   73 Jan 18 14:42 ..
-rw-r--r--  1 mthomas use300 1543 Jul 17  2018 filelisting.txt
-rw-r--r--  1 mthomas use300    0 Jan 18 15:12 myfile1.txt
-rw-r--r--  1 mthomas use300    0 Jan 18 15:12 newfile.txt
```
To delete a file, use the `rm` (remove command):

```
[mthomas@comet-ln2 testdir]$ rm myfile1.txt
(base) [mthomas@comet-ln2:~/testdir] rm myfile1.txt 
(base) [mthomas@comet-ln2:~/testdir] ls -al
total 84
drwxr-xr-x  2 mthomas use300    4 Jan 18 15:15 .
drwxr-x--- 47 mthomas use300   73 Jan 18 14:42 ..
-rw-r--r--  1 mthomas use300 1543 Jul 17  2018 filelisting.txt
-rw-r--r--  1 mthomas use300    0 Jan 18 15:12 newfile.txt
```

[Back to Top](#top)
<hr>

### <a name="directories">Directories</a>

A common task in computing is to work with examples and collaborator files. Suppose we want to copy the contents of another directory to our local directory. On Comet, there is a large suite of applications that you can work with. In this example, we will copy files from the HPCT user training directory.

First, we will make a folder to hold comet examples and then `cd` into that new directory. This is done using the `mkdir` command:
```
[mthomas@comet-ln2 ~]$ mkdir comet-examples
[mthomas@comet-ln2 ~]$ ls -al            
total 166
drwxr-x---   8 mthomas use300    24 Jul 17 20:20 .
drwxr-xr-x 139 root    root       0 Jul 17 20:17 ..
-rw-r--r--   1 mthomas use300  2487 Jun 23  2017 .alias
-rw-------   1 mthomas use300 14247 Jul 17 12:11 .bash_history
-rw-r--r--   1 mthomas use300    18 Jun 19  2017 .bash_logout
-rw-r--r--   1 mthomas use300   176 Jun 19  2017 .bash_profile
-rw-r--r--   1 mthomas use300   159 Jul 17 18:24 .bashrc
drwxr-xr-x   2 mthomas use300     2 Jul 17 20:20 comet-examples
[snip extra lines]
[mthomas@comet-ln2 ~]$ cd comet-examples/
[mthomas@comet-ln2 comet-examples]$ pwd
/home/mthomas/comet-examples
[mthomas@comet-ln2 comet-examples]$
```
Next, we will look at the directory where some course examples are locacted: 
```
(base) [mthomas@comet-ln2:~/HPCT] ls -al /home/mthomas/HPCT
total 131
drwxr-xr-x  5 mthomas use300  5 Jan 18 15:31 .
drwxr-x--- 49 mthomas use300 75 Jan 18 15:44 ..
drwxr-xr-x  2 mthomas use300 15 Jan 18 15:31 CUDA
drwxr-xr-x  2 mthomas use300  7 Jan 18 15:45 MPI
drwxr-xr-x  2 mthomas use300 10 Jan 18 15:30 OPENMP
```
To copy a single file to the `comet-examples` directory, we need to use the full path for the "source" file. Suppose we want to just copy the MPI fortran file:
```
(base) [mthomas@comet-ln2:~/HPCT] ls -al /home/mthomas/HPCT/MPI
total 506
drwxr-xr-x 2 mthomas use300      7 Jan 18 15:45 .
drwxr-xr-x 5 mthomas use300      5 Jan 18 15:31 ..
-rwxr-xr-x 1 mthomas use300 750288 Jan 18 15:35 hello_mpi
-rw-r--r-- 1 mthomas use300   2786 Jan 18 15:45 hello_mpi.30939844.comet-14-02.out
-rw-r--r-- 1 mthomas use300    336 Jan 18 15:35 hello_mpi.f90
-rw-r--r-- 1 mthomas use300    341 Jan 18 15:44 hello_mpi.sb
-rw-r--r-- 1 mthomas use300    393 Jan 18 15:30 hello_mpi_SI19.sb
(base) [mthomas@comet-ln2:~/HPCT] ls -al /home/mthomas/HPCT/MPI/hello_mpi.f90 
-rw-r--r-- 1 mthomas use300 336 Jan 18 15:35 /home/mthomas/HPCT/MPI/hello_mpi.f90
```
In this example, we will copy a single mpi file from the `source` directory, /home/mthomas/HPCT/MPI/, to
the `destination` directory, which in this case is the current working directory. You can discover what the current working directory using the `pwd` command (print working directory):
```
(base) [mthomas@comet-ln2:~/comet-examples] cd ~/comet-examples
(base) [mthomas@comet-ln2:~/comet-examples] pwd
/home/mthomas/comet-examples
(base) [mthomas@comet-ln2:~/comet-examples] ls -al
total 74
drwxr-xr-x  2 mthomas use300  2 Jan 18 15:22 .
drwxr-x--- 49 mthomas use300 75 Jan 18 15:44 ..
```
To copy the source file to this directory, use the `cp` command:
```
(base) [mthomas@comet-ln2:~/comet-examples] cp /home/mthomas/HPCT/MPI/hello_mpi.f90  /home/mthomas/comet-examples/hello_mpi.f90 
(base) [mthomas@comet-ln2:~/comet-examples] ls -al
total 84
drwxr-xr-x  2 mthomas use300   3 Jan 18 16:06 .
drwxr-x--- 49 mthomas use300  75 Jan 18 15:44 ..
-rw-r--r--  1 mthomas use300 336 Jan 18 16:06 hello_mpi.f90
```
Note that for the file copy, we used the `full path` for both the `source` file and the `destination file.` Recall that for Unix/Linux a single dot, `.` represents the current working directory, and  double dots, `..` represent the directory above. This can be used to simplify commands like the copy command:
```
(base) [mthomas@comet-ln2:~/comet-examples] cp /home/mthomas/HPCT/MPI/hello_mpi.f90  .
(base) [mthomas@comet-ln2:~/comet-examples] ls -al
total 84
drwxr-xr-x  2 mthomas use300   3 Jan 18 16:06 .
drwxr-x--- 49 mthomas use300  75 Jan 18 15:44 ..
-rw-r--r--  1 mthomas use300 336 Jan 18 16:12 hello_mpi.f90
```
You can also copy and rename the source file:
```
(base) [mthomas@comet-ln2:~/comet-examples] cp /home/mthomas/HPCT/MPI/hello_mpi.f90  hello_mpi_V2.f90
(base) [mthomas@comet-ln2:~/comet-examples] ls -al
total 84
drwxr-xr-x  2 mthomas use300   4 Jan 18 16:13 .
drwxr-x--- 49 mthomas use300  75 Jan 18 15:44 ..
-rw-r--r--  1 mthomas use300 336 Jan 18 16:12 hello_mpi.f90
-rw-r--r--  1 mthomas use300 336 Jan 18 16:13 hello_mpi_V2.f90
```
[Back to Top](#top)
<hr>

In this case we have a copy of one file from the training files. To copy a large number files, we can copy the director and subdirectories if desired. Copies of directories use the same command: `cp`. 
For a large number of files, it is easier to copy the entire directory using the `-R` or `-r` recursive command.
```
(base) [mthomas@comet-ln2:~/comet-examples] cp -r /home/mthomas/HPCT .
(base) [mthomas@comet-ln2:~/comet-examples] ll
total 94
drwxr-xr-x  3 mthomas use300   5 Jan 18 16:16 .
drwxr-x--- 49 mthomas use300  75 Jan 18 15:44 ..
-rw-r--r--  1 mthomas use300 336 Jan 18 16:12 hello_mpi.f90
-rw-r--r--  1 mthomas use300 336 Jan 18 16:13 hello_mpi_V2.f90
drwxr-xr-x  5 mthomas use300   5 Jan 18 16:16 HPCT
(base) [mthomas@comet-ln2:~/comet-examples] ls -al HPCT/
total 58
drwxr-xr-x 5 mthomas use300  5 Jan 18 16:16 .
drwxr-xr-x 3 mthomas use300  5 Jan 18 16:16 ..
drwxr-xr-x 2 mthomas use300 15 Jan 18 16:16 CUDA
drwxr-xr-x 2 mthomas use300  7 Jan 18 16:16 MPI
drwxr-xr-x 2 mthomas use300 10 Jan 18 16:16 OPENMP
```
Add the `-p` option to preserve the file dates:
```
(base) [mthomas@comet-ln2:~/comet-examples] cp -r -p /home/mthomas/HPCT .
(base) [mthomas@comet-ln2:~/comet-examples] ls -al
total 94
drwxr-xr-x  3 mthomas use300   5 Jan 18 16:16 .
drwxr-x--- 49 mthomas use300  75 Jan 18 15:44 ..
-rw-r--r--  1 mthomas use300 336 Jan 18 16:12 hello_mpi.f90
-rw-r--r--  1 mthomas use300 336 Jan 18 16:13 hello_mpi_V2.f90
drwxr-xr-x  5 mthomas use300   5 Jan 18 15:31 HPCT
(base) [mthomas@comet-ln2:~/comet-examples] ls -al HPCT/
total 58
drwxr-xr-x 5 mthomas use300  5 Jan 18 15:31 .
drwxr-xr-x 3 mthomas use300  5 Jan 18 16:16 ..
drwxr-xr-x 2 mthomas use300 15 Jan 18 15:31 CUDA
drwxr-xr-x 2 mthomas use300  7 Jan 18 15:45 MPI
drwxr-xr-x 2 mthomas use300 10 Jan 18 15:30 OPENMP
```
There are several things to observe with this command:
1. The owner of these new files is the user who ran the commands (mthomas).
2. The use of the `-r` argument is a recursive copy, which gets all files in the directory.
3. The use of the `-p` arguement preserves the date/timestamp, which can be helpful but not always required.
4. The use of one of the special _dot_ characters,  \. in the command above: the syntax tells the operating system to copy all contents of the _/home/mthomas/HPCT/_ directory to the `.` directory, or the current directory.

To copy a directory and give it a new name:
```
(base) [mthomas@comet-ln2:~/comet-examples] cp -r -p /home/mthomas/HPCT FOOBAR
(base) [mthomas@comet-ln2:~/comet-examples] ls -al
total 94
drwxr-xr-x  4 mthomas use300   6 Jan 18 16:20 .
drwxr-x--- 49 mthomas use300  75 Jan 18 15:44 ..
drwxr-xr-x  5 mthomas use300   5 Jan 18 15:31 FOOBAR
-rw-r--r--  1 mthomas use300 336 Jan 18 16:12 hello_mpi.f90
-rw-r--r--  1 mthomas use300 336 Jan 18 16:13 hello_mpi_V2.f90
drwxr-xr-x  5 mthomas use300   5 Jan 18 15:31 HPCT
(base) [mthomas@comet-ln2:~/comet-examples] ls -al FOOBAR/
total 58
drwxr-xr-x 5 mthomas use300  5 Jan 18 15:31 .
drwxr-xr-x 4 mthomas use300  6 Jan 18 16:20 ..
drwxr-xr-x 2 mthomas use300 15 Jan 18 15:31 CUDA
drwxr-xr-x 2 mthomas use300  7 Jan 18 15:45 MPI
drwxr-xr-x 2 mthomas use300 10 Jan 18 15:30 OPENMP
```
You can rename a directory using the `mv` command:
```
(base) [mthomas@comet-ln2:~/comet-examples] mv FOOBAR/  HPCT_DUP
(base) [mthomas@comet-ln2:~/comet-examples] ls -al
total 94
drwxr-xr-x  4 mthomas use300   6 Jan 18 16:21 .
drwxr-x--- 49 mthomas use300  75 Jan 18 15:44 ..
-rw-r--r--  1 mthomas use300 336 Jan 18 16:12 hello_mpi.f90
-rw-r--r--  1 mthomas use300 336 Jan 18 16:13 hello_mpi_V2.f90
drwxr-xr-x  5 mthomas use300   5 Jan 18 15:31 HPCT
drwxr-xr-x  5 mthomas use300   5 Jan 18 15:31 HPCT_DUP
(base) [mthomas@comet-ln2:~/comet-examples] ls -al HPCT_DUP/
total 58
drwxr-xr-x 5 mthomas use300  5 Jan 18 15:31 .
drwxr-xr-x 4 mthomas use300  6 Jan 18 16:21 ..
drwxr-xr-x 2 mthomas use300 15 Jan 18 15:31 CUDA
drwxr-xr-x 2 mthomas use300  7 Jan 18 15:45 MPI
drwxr-xr-x 2 mthomas use300 10 Jan 18 15:30 OPENMP
```
To move to the directory, use the `cd` (change directory)
```
(base) [mthomas@comet-ln2:~/comet-examples] pwd
/home/mthomas/comet-examples
(base) [mthomas@comet-ln2:~/comet-examples] cd HPCT/MPI
(base) [mthomas@comet-ln2:~/comet-examples/HPCT/MPI] pwd
/home/mthomas/comet-examples/HPCT/MPI
(base) [mthomas@comet-ln2:~/comet-examples/HPCT/MPI] ls -al
total 506
drwxr-xr-x 2 mthomas use300      7 Jan 18 15:45 .
drwxr-xr-x 5 mthomas use300      5 Jan 18 15:31 ..
-rwxr-xr-x 1 mthomas use300 750288 Jan 18 15:35 hello_mpi
-rw-r--r-- 1 mthomas use300   2786 Jan 18 15:45 hello_mpi.30939844.comet-14-02.out
-rw-r--r-- 1 mthomas use300    336 Jan 18 15:35 hello_mpi.f90
-rw-r--r-- 1 mthomas use300    341 Jan 18 15:44 hello_mpi.sb
-rw-r--r-- 1 mthomas use300    393 Jan 18 15:30 hello_mpi_SI19.sb
```
You can sort the order of the file listings by date (or size or other fields -- see the `man` pages). The default file listing in alphabetic, to  see the files in chronological order (or reverse):
```
(base) [mthomas@comet-ln2:~/comet-examples/HPCT/MPI] ls -alt
total 506
-rw-r--r-- 1 mthomas use300   2786 Jan 18 15:45 hello_mpi.30939844.comet-14-02.out
drwxr-xr-x 2 mthomas use300      7 Jan 18 15:45 .
-rw-r--r-- 1 mthomas use300    341 Jan 18 15:44 hello_mpi.sb
-rwxr-xr-x 1 mthomas use300 750288 Jan 18 15:35 hello_mpi
-rw-r--r-- 1 mthomas use300    336 Jan 18 15:35 hello_mpi.f90
drwxr-xr-x 5 mthomas use300      5 Jan 18 15:31 ..
-rw-r--r-- 1 mthomas use300    393 Jan 18 15:30 hello_mpi_SI19.sb

(base) [mthomas@comet-ln2:~/comet-examples/HPCT/MPI] ls -alrt
total 506
-rw-r--r-- 1 mthomas use300    393 Jan 18 15:30 hello_mpi_SI19.sb
drwxr-xr-x 5 mthomas use300      5 Jan 18 15:31 ..
-rw-r--r-- 1 mthomas use300    336 Jan 18 15:35 hello_mpi.f90
-rwxr-xr-x 1 mthomas use300 750288 Jan 18 15:35 hello_mpi
-rw-r--r-- 1 mthomas use300    341 Jan 18 15:44 hello_mpi.sb
drwxr-xr-x 2 mthomas use300      7 Jan 18 15:45 .
-rw-r--r-- 1 mthomas use300   2786 Jan 18 15:45 hello_mpi.30939844.comet-14-02.out
```

[Back to Top](#top)
<hr>

## <a name="permissions">Permissions</a>
In the section we will look breifly at how to file permissions. Before you can change the file permissions, you need to own it or have permission as a group member. For a more detailed tutorial, see http://www.nersc.gov/users/storage-and-file-systems/unix-file-permissions/. Permissions are written in the first column, with fields that specify whether or not the file is a directory (`d`), what the read/write/execution permissions (`rwx`) for the files are for users and groups.  Using the example below:

```
(base) [mthomas@comet-ln2:~/comet-examples/HPCT/MPI] ls -al
total 506
drwxr-xr-x 2 mthomas use300      7 Jan 18 15:45 .
drwxr-xr-x 5 mthomas use300      5 Jan 18 15:31 ..
-rwxr-xr-x 1 mthomas use300 750288 Jan 18 15:35 hello_mpi
-rw-r--r-- 1 mthomas use300   2786 Jan 18 15:45 hello_mpi.30939844.comet-14-02.out
-rw-r--r-- 1 mthomas use300    336 Jan 18 15:35 hello_mpi.f90
-rw-r--r-- 1 mthomas use300    341 Jan 18 15:44 hello_mpi.sb
-rw-r--r-- 1 mthomas use300    393 Jan 18 15:30 hello_mpi_SI19.sb
```
The order of the markers are grouped into 4 fields:
`-` `rwx` `r-x` `r-x`
* Field 1 == directory, a `d` or `-` means directory or not a directory
* Field 2 == owner permissions 'rwx' means the owner can read, write, and exectute
* Field 3 == group permissions 'rwx' means the owner can read and exectute, but not modify
* Field 4 == other/world permissions 'r-x' means the others can read and exectute, but not modiry

To change the file access permissions, use the `chmod` command. In the file listing above:
* only user mthomas has permission to edit (`rw-`) the text files or to execute (`rwx`) the binary (hello_mpi) files, 
* members of the groups "use300" and "others" have read only permission ("r--"). There are several ways to modify permissions, we will use the binary representation where the rwx status represents a binary number 2^n, where n is the position of the permission starting from the right. For example:
```
  r-- = 2^2 + 0 + 0 = 4 + 0 + 0 = 4
  rw- = 2^2 + 2^1 + 0 = 4 + 2 + 0 = 6
  r-x = 2^2 + 0 + 2^0 = 4 + 0 + 1 = 5
  rwx = 2^2 + 2^1 + 2^0 = 4 + 2 + 1 = 7
```

In the example below, we will set read and write permissions to the owner and the group, and limit the other/world group to read only:
```
(base) [mthomas@comet-ln2:~/comet-examples/HPCT/MPI] chmod 660 *
(base) [mthomas@comet-ln2:~/comet-examples/HPCT/MPI] ls -al
total 506
drwxr-xr-x 2 mthomas use300      7 Jan 18 15:45 .
drwxr-xr-x 5 mthomas use300      5 Jan 18 15:31 ..
-rw-rw---- 1 mthomas use300 750288 Jan 18 15:35 hello_mpi
-rw-rw---- 1 mthomas use300   2786 Jan 18 15:45 hello_mpi.30939844.comet-14-02.out
-rw-rw---- 1 mthomas use300    336 Jan 18 15:35 hello_mpi.f90
-rw-rw---- 1 mthomas use300    341 Jan 18 15:44 hello_mpi.sb
-rw-rw---- 1 mthomas use300    393 Jan 18 15:30 hello_mpi_SI19.sb
```
In the example above, we use the star wildcard, \" \* \" to represent all the files in the directory (See the section on wildcards below). We can use the wildcard to **change the group** of some of the files. For example, to change the group of only the \*.out files so that the members of a group can access the files, and no others:

```
[mthomas@comet-ln2 OPENMP]$ groups
use300 sdsc sdu233 [snip] ...
(base) [mthomas@comet-ln2:~/comet-examples/HPCT/MPI] chgrp sdu233 *.out
(base) [mthomas@comet-ln2:~/comet-examples/HPCT/MPI] ls -al
total 506
drwxr-xr-x 2 mthomas use300      7 Jan 18 15:45 .
drwxr-xr-x 5 mthomas use300      5 Jan 18 15:31 ..
-rw-rw---- 1 mthomas use300 750288 Jan 18 15:35 hello_mpi
-rw-rw---- 1 mthomas sdu233   2786 Jan 18 15:45 hello_mpi.30939844.comet-14-02.out
-rw-rw---- 1 mthomas use300    336 Jan 18 15:35 hello_mpi.f90
-rw-rw---- 1 mthomas use300    341 Jan 18 15:44 hello_mpi.sb
-rw-rw---- 1 mthomas use300    393 Jan 18 15:30 hello_mpi_SI19.sb

```
 
[Back to Top](#top)
<hr>

## <a name="common-utilities">Common Utilities</a>
 common utilities: grep, cat, less, head, sort, tar, gzip ,and pigz
