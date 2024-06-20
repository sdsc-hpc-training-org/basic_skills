# Using SDSC HPC Resources:  Basic Linux Skills on Expanse
[//]: # " Comment example "

[//]: # ( Comment2 )

When you log on to [Expanse](https://expanse.sdsc.edu), your computer operating system will be a Linux or Unix shell. \"_A Unix shell is a command-line interpreter or shell that provides a traditional Unix-like command line user interface. This environment is very different from the easy to use GUI interfaces we have all become used in the Windows and MacOS systems_\" (https://en.wikipedia.org/wiki/Unix_shell).

Basic Linux skills are necessary to complete the hands-on exercises. If it’s been a while since you’ve worked in a Linux environment, be sure to reacquaint yourself with the following topic (many of which are demonstrated below)s: copying, listing, deleting and renaming files; using wildcards; navigating directories; changing file permissions; setting environment variables; using common utilities (grep, cat, less, head, sort, tar, gzip). 

This tutorial is focussed on using Linux on the SDSC Expanse supercomputer. There a a lot of other tutorial on the Web:
* A nice tutorial can be found here http://www.ee.surrey.ac.uk/Teaching/Unix/. You should also be comfortable with one of the standard Linux editors, such as vim, emacs, or nano.
* For a fun tutorial on Linux, see the UCSD/SDSC Supercomputing Club's tutorial, based on a Google community project, here: https://supercomputing-club.sdsc.edu/posts/advent-of-scc-2023/advent-of-scc-epilogue/

Notes:
* For the examples below, we are using the `bash` shell, which is the default shell for new accounts on Expanse. For the purposes of following SDSC tutorials and exercises, please do not change the shell.
* For any Linux command, you can find out what it does by asking for help. The syntax is usually
  * `command` --help  
  * man `command`  --> invokes a user guide or manual
  * search the web using google or some other search engine
* In Linux/Unix, everything is a file: a text file, a directory, even the output for a command
* Linux/Unix is case sensitive.
  
<a name="top">**Examples::**
* [Basic Environment](#basic-env)
* [Directories and Navigation](#dirs-and-nav)
* [Copying directories](#copydir)
* [Files](#files)
* [Permissions](#permissions)
* [Wildcards](#wildcards)
* [Common Utilities](#common-utilities)


Note: if you have difficulties completing this task, please contact staff at <consult@sdsc.edu>.
<hr>

## <a name="basic-env">Basic Environment</a>
Using Unix commands, we can learn a lot about the machine we are logged onto. Some of the commands are simple:

```
[username@login02 ~]$ date
Tue Jan 16 20:20:23 PST 2024
[username@login02 ~]$ hostname
login02
[username@login02 ~]$ whoami
username
```
Note: To learn about most unix commands, try accessing the `man` pages:
``` sh
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

The unix command `env` will print out the _environment_ settings for your login session.
The list below is an edited summary of all the information
Warning: the output can be very long (over 90 lines)
```
[username@login02 ~]$ env
MODULEPATH=/opt/modulefiles/mpi/.intel:/opt/modulefiles/applications/.intel:/opt/modulefiles/mpi:/opt/modulefiles/compilers:/opt/modulefiles/applications:/usr/share/Modules/modulefiles:/etc/modulefiles
LOADEDMODULES=intel/2013_sp1.2.144:mvapich2_ib/2.1:gnutools/2.69
HOME=/home/username
SDSCHOME=/opt/sdsc
LOGNAME=username
SSH_CONNECTION=xxx.xxx.xx.xx 53640 198.202.113.253 22
DISPLAY=localhost:48.0
```
It is often useful to print out (or use) environment variables. To print them out, use the `echo` command, and `$` sign (which extracts the value of the shell variable):
```
[username@login02 ~]$ echo $SHELL
/bin/bash
[username@login02 ~]$ echo $HOME
/home/username
```
Another important environment variable is the home directory variable, the \"tilde\" character:  `~`
```
[username@login02 ~]$ echo ~
/home/username
[username@login02 ~]$
```
You can create your own environment variables:
```
[username@login02 ~]$ MY_NAME="Super User"
[username@login02 ~]$ echo $MY_NAME
Super User
```

Unix has the concept of users and groups. Groups are used to control access to resources (files, applications, etc.) and help establish a secure envionment Users can be in more than one group. To see which groups you are a member of, use the `group` command:
```
[username@login02 OPENMP]$ groups
abc123 pet heart scicom-docs grdclus webwrt scwpf ...
```

[Back to Top](#top)
<hr>



## Directories and Navigation<a name="dirs-and-nav"></a>

In unix, everything is a file, which can be confusing at first. The locations for where files are stored   are called directories (which is equivalent to folders), and are also viewed as files by the operating system. To find out where you are in the system, use the `pwd` command (print working directory), which prints the full path to the directory you are currently in:
```
[username@login02 ~]$ pwd
/home/username
```
To see what are the contents of the current directory are, use the file listing command `ls`
```
[username@login02 ~]$ ls
filelisting.txt intel   loadgccomgnuenv.sh  loadgnuenv.sh	loadintelenv.sh  tools
```
In every Unix directory, there are \"hidden\" files (just like on Macs and Windows machines), to see them, run the `ls -a` command:
```
[username@login02 ~]$ ls -a
.	.bash_history  .bashrc	 .gitconfig  loadgccomgnuenv.sh  .ncviewrc     .ssh	 .vimrc
..	.bash_logout   .config filelisting.txt	 intel	     loadgnuenv.sh	 .petscconfig  tools	 .Xauthority
.alias	.bash_profile    .kshrc      loadintelenv.sh	 .slurm        .viminfo
```
In Unix, sometimes it is hard tell if a file is a directory. To see file details (including timestamp and size), run the `ls -l` command:
```
[username@login02 ~]$ ls -l
-rw-r--r-- 1 username abc123 322 Jul 17 21:04 filelisting.txt
drwxr-xr-x 3 username abc123   3 Jun 22  2023 intel
-rwx------ 1 username abc123 101 Jun 27  2023 loadgccomgnuenv.sh
-rwx------ 1 username abc123  77 Oct 16  2023 loadgnuenv.sh
-rwxr-xr-x 1 username abc123 125 Oct 16  2023 loadintelenv.sh
drwxr-xr-x 2 username abc123   4 Jun 30  2023 tools
```
You can combine the two commands above and use it to see the full directory and file information:
```
[username@login02 ~]$ ls -al
total 166
drwx------   7 username abc123    23 Jul 17 19:33 .
drwxr-xr-x 143 root    root       0 Jul 17 20:01 ..
-rw-r--r--   1 username abc123  2487 Jun 23  2023 .alias
-rw-------   1 username abc123 14247 Jul 17 12:11 .bash_history
-rw-r--r--   1 username abc123    18 Jun 19  2023 .bash_logout
-rw-r--r--   1 username abc123   176 Jun 19  2023 .bash_profile
-rw-r--r--   1 username abc123   159 Jul 17 18:24 .bashrc
drwx------   3 username abc123     3 Oct 23  2023 .config
-rw-r--r--   1 username abc123  322 Jul 17 21:04 filelisting.txt
-rw-r--r--   1 username abc123  1641 Jun 22  2023 .gccomrc
-rw-r--r--   1 username abc123   245 Jun 28  2023 .gitconfig
drwxr-xr-x   3 username abc123     3 Jun 22  2023 intel
-rw-r--r--   1 username abc123   171 Jun 19  2023 .kshrc
-rwx------   1 username abc123   101 Jun 27  2023 loadgccomgnuenv.sh
-rwx------   1 username abc123    77 Oct 16  2023 loadgnuenv.sh
-rwxr-xr-x   1 username abc123   125 Oct 16  2023 loadintelenv.sh
[snip extra lines]
```
There are several things to notice in the above listing: the first column of data is information about the file "permissions\", which controls who can see/read/modify what files (`r`=read, `w`=write,`x`=execute,`-`=no permission); the next 2 columns are the username and groupID; the 3rd and 4th columns are the size and date. This is discussed in more detail in the [Permissions](#permissions) section below. Also, note that two files have `dots` for their names: in unix the "dot" is a component of a filename. When working with filenames, a leading dot is the prefix of a "hidden" file, a file that an `ls` will not normally show. But also, the single dot, `.` represents the current working directory, and the double dots, `..` represent the directory above. You use these as arguments to unix commands dealing with directories.

There are simple Linux commands to create and remove directories, and to populate the directories.
To create a directory, use the `mkdir`, make directory command (more about directories in the sections below):
```
[username@login02 ~]$ mkdir testdir
[username@login02 ~]$ ls -l
total 12
drwxr-xr-x 3 username abc123   3 Jun 22  2023 intel
-rwx------ 1 username abc123 101 Jun 27  2023 loadgccomgnuenv.sh
-rwx------ 1 username abc123  77 Oct 16  2023 loadgnuenv.sh
-rwxr-xr-x 1 username abc123 125 Oct 16  2023 loadintelenv.sh
drwxr-xr-x 2 username abc123   2 Jul 17 20:49 testdir
drwxr-xr-x 2 username abc123   4 Jun 30  2023 tools
```
To move into that directory, use the `cd`, change directory command:
```
[username@login02 ~]$ cd testdir/
[username@login02 testdir]$ ls -al
total 20
drwxr-xr-x 2 username abc123  2 Jul 17 20:49 .
drwxr-x--- 9 username abc123 25 Jul 17 20:49 ..
[username@login02 testdir]$
```
From this directory, you can use the `..` command to see the contents of the directory above:

```
[username@login02 testdir]$ ls -l ..
[username@login02 testdir]$ /bin/ls -l ..
total 22
drwxr-xr-x 4 username abc123    5 Jul 17 20:43 expanse-examples
-rw-r--r-- 1 username abc123 322 Jul 17 21:04 filelisting.txt
drwxr-xr-x 3 username abc123    3 Jun 22  2023 intel
-rwx------ 1 username abc123  101 Jun 27  2023 loadgccomgnuenv.sh
-rwx------ 1 username abc123   77 Oct 16  2023 loadgnuenv.sh
-rwxr-xr-x 1 username abc123  125 Oct 16  2023 loadintelenv.sh
drwxr-xr-x 2 username abc123    4 Jul 17 20:53 testdir
drwxr-xr-x 2 username abc123    4 Jun 30  2023 tools
```
To remove files and directories there are different mechanisms, depending on whether or not the directory is empty or contains files. For this example, we create a new directory, `testdir2`, we'll create three directories using the `mkdir` command, populate some testfiles using the `touch` command, and then try to delete the directories using either the `rmdir` or `rm` commands.
```
[username@login01 testdir]$cd ..
[username@login01 testdir]$ mkdir testdir2
[username@login01 testdir]$ cd testdir2
[username@login01 testdir2]$ mkdir dir1
[username@login01 testdir2]$ mkdir dir2
[username@login01 testdir2]$ mkdir dir3
[username@login01 testdir2]$ ll
total 71
drwxr-xr-x  5 username use300  5 Jan 17 22:11 .
drwxr-x--- 50 username use300 91 Jan 17 22:01 ..
drwxr-xr-x  2 username use300  2 Jan 17 22:11 dir1
drwxr-xr-x  2 username use300  2 Jan 17 22:11 dir2
drwxr-xr-x  2 username use300  2 Jan 17 22:11 dir3
```
Next, create some testfiles using the `touch` command:
```
[username@login01 testdir2]$ touch f1
[username@login01 testdir2]$ touch f2
[username@login01 testdir2]$ touch f3
[username@login01 testdir2]$ touch dir2/file1
[username@login01 testdir2]$ touch dir2/file2
[username@login01 testdir2]$ touch dir2/file3
[username@login01 testdir2]$ ls -al
total 90
drwxr-xr-x  5 username use300  8 Jan 17 22:23 .
drwxr-x--- 50 username use300 91 Jan 17 22:01 ..
drwxr-xr-x  2 username use300  5 Jan 17 22:23 dir1
drwxr-xr-x  2 username use300  5 Jan 17 22:17 dir2
drwxr-xr-x  2 username use300  5 Jan 17 22:18 dir3
-rw-r--r--  1 username use300  0 Jan 17 22:23 f1
-rw-r--r--  1 username use300  0 Jan 17 22:23 f2
-rw-r--r--  1 username use300  0 Jan 17 22:23 f3
[username@login01 testdir2]$ ls -al dir2
total 3
drwxr-xr-x 2 username use300 5 Jan 17 22:17 .
drwxr-xr-x 4 username use300 4 Jan 17 22:12 ..
-rw-r--r-- 1 username use300 0 Jan 17 22:16 file1
-rw-r--r-- 1 username use300 0 Jan 17 22:16 file2
-rw-r--r-- 1 username use300 0 Jan 17 22:17 file3
```
For a file, we use the remove, `rm` command:
```
[username@login01 testdir2]$ 
[username@login01 testdir2]$ rm f3
[username@login01 testdir2]$ ll -al
total 72
drwxr-xr-x  5 username use300  7 Jan 17 22:31 .
drwxr-x--- 50 username use300 91 Jan 17 22:01 ..
drwxr-xr-x  2 username use300  5 Jan 17 22:23 dir1
drwxr-xr-x  2 username use300  5 Jan 17 22:17 dir2
drwxr-xr-x  2 username use300  5 Jan 17 22:18 dir3
-rw-r--r--  1 username use300  0 Jan 17 22:23 f1
-rw-r--r--  1 username use300  0 Jan 17 22:23 f2

```
For an *empty* directory, we can use the `rmdir` command:
```
[username@login01 testdir2]$ ls -al dir1
total 1
drwxr-xr-x 2 username use300 2 Jan 17 22:11 .
drwxr-xr-x 5 username use300 5 Jan 17 22:11 ..
[username@login01 testdir2]$ rm dir1
rm: cannot remove 'dir1': Is a directory
[username@login01 testdir2]$ rmdir dir1
[username@login01 testdir2]$ ll
total 71
drwxr-xr-x  4 username use300  4 Jan 17 22:12 .
drwxr-x--- 50 username use300 91 Jan 17 22:01 ..
drwxr-xr-x  2 username use300  2 Jan 17 22:11 dir2
drwxr-xr-x  2 username use300  2 Jan 17 22:11 dir3

```
If the directory has contents (files or subdirectories), you use the 'rm' command with arguments to *force* the removal of the directory and all of its contents:
```
[username@login01 testdir2]$ ll dir3
total 3
drwxr-xr-x 2 username use300 5 Jan 17 22:18 .
drwxr-xr-x 5 username use300 7 Jan 17 22:31 ..
-rw-r--r-- 1 username use300 0 Jan 17 22:18 file31
-rw-r--r-- 1 username use300 0 Jan 17 22:18 file32
-rw-r--r-- 1 username use300 0 Jan 17 22:18 file33
[username@login01 testdir2]$ rmdir dir3
rmdir: failed to remove 'dir3': Directory not empty
[username@login01 testdir2]$ rm dir3
rm: cannot remove 'dir3': Is a directory
[username@login01 testdir2]$ rm -f dir3
rm: cannot remove 'dir3': Is a directory
[username@login01 testdir2]$ rm -rf dir3
[username@login01 testdir2]$ ls -al
total 72
drwxr-xr-x  4 username use300  6 Jan 17 23:01 .
drwxr-x--- 50 username use300 91 Jan 17 22:01 ..
drwxr-xr-x  2 username use300  5 Jan 17 22:23 dir1
drwxr-xr-x  2 username use300  5 Jan 17 22:17 dir2
-rw-r--r--  1 username use300  0 Jan 17 22:23 f1
-rw-r--r--  1 username use300  0 Jan 17 22:23 f2
```

[Back to Top](#top)
<hr>

## Copying directories<a name="copydir"></a>

A common task in computing is to work with examples and collaborator files. Suppose we want to copy the contents of another directory to our local directory. On Expanse, there is a large suite of applications that you can work with. In this example, we will copy the GPU application folder. Suppose you are interested in working with one of the files or directories in the /share/apps/examples/ directory.

First, we will make a folder to hold expanse examples and then `cd` into that new directory. This is done using the `mkdir` command:
```
[username@login02 ~]$ mkdir expanse-examples
[username@login02 ~]$ ls -al            
total 166
drwxr-x---   8 username abc123    24 Jul 17 20:20 .
drwxr-xr-x 139 root    root       0 Jul 17 20:17 ..
-rw-r--r--   1 username abc123  2487 Jun 23  2023 .alias
-rw-------   1 username abc123 14247 Jul 17 12:11 .bash_history
-rw-r--r--   1 username abc123    18 Jun 19  2023 .bash_logout
-rw-r--r--   1 username abc123   176 Jun 19  2023 .bash_profile
-rw-r--r--   1 username abc123   159 Jul 17 18:24 .bashrc
drwxr-xr-x   2 username abc123     2 Jul 17 20:20 expanse-examples
[snip extra lines]
[username@login02 ~]$ cd expanse-examples/
[username@login02 expanse-examples]$ pwd
/home/username/expanse-examples
[username@login02 expanse-examples]$
```

Next, we will look at the directory where the OPENMP code is stored:
```
[username@login02 ~]$ ls -al /share/apps/examples/OPENMP/
total 740
drwxrwxr-x  2 mahidhar abc123   4096 Mar 12 08:54 .
drwxrwxr-x 56 mahidhar abc123   4096 May 14 18:11 ..
-rwxr-xr-x  1 mahidhar abc123 728112 Apr 15  2015 hello_openmp
-rw-r--r--  1 mahidhar abc123    984 Apr 15  2015 hello_openmp.500005.expanse-27-01.out
-rw-r--r--  1 mahidhar abc123    247 Apr 15  2015 hello_openmp.f90
-rw-r--r--  1 mahidhar abc123    656 Apr 22  2015 hello_openmp_shared.508392.expanse-11-01.out
-rw-r--r--  1 mahidhar abc123    310 Apr 15  2015 openmp-slurm.sb
-rw-r--r--  1 mahidhar abc123    347 Apr 22  2015 openmp-slurm-shared.sb
```
Copies of files and directories use the same command: `cp`. To copy a single file to the `expanse-examples` directory, we need to use the full path:

```sh
[username@login02 expanse-examples]$ cp /share/apps/examples/OPENMP/hello_openmp.f90 hello_openmp.f90
[username@login02 expanse-examples]$ ls -al
total 29
drwxr-xr-x 2 username abc123   3 Jul 17 20:24 .
drwxr-x--- 8 username abc123  24 Jul 17 20:20 ..
-rw-r--r-- 1 username abc123 247 Jul 17 20:24 hello_openmp.f90

```
For a large number of files, it is easier to copy the entire directory using the `-R` or `-r` recursive command:

```
[username@login02 expanse-examples]$ cp -r -p /share/apps/examples/OPENMP/ .
[username@login02 expanse-examples]$ ll
total 48
drwxr-xr-x 3 username abc123   4 Jul 17 20:26 .
drwxr-x--- 8 username abc123  24 Jul 17 20:20 ..
-rw-r--r-- 1 username abc123 247 Jul 17 20:24 hello_openmp.f90
drwxr-xr-x 2 username abc123   8 Jul 17 20:26 OPENMP
[username@login02 expanse-examples]$ ls -al OPENMP/
total 479
drwxrwxr-x 2 username abc123      8 Mar 12 08:54 .
drwxr-xr-x 3 username abc123      4 Jul 17 20:32 ..
-rwxr-xr-x 1 username abc123 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 username abc123    984 Apr 15  2015 hello_openmp.500005.expanse-27-01.out
-rw-r--r-- 1 username abc123    247 Apr 15  2015 hello_openmp.f90
-rw-r--r-- 1 username abc123    656 Apr 22  2015 hello_openmp_shared.508392.expanse-11-01.out
-rw-r--r-- 1 username abc123    310 Apr 15  2015 openmp-slurm.sb
-rw-r--r-- 1 username abc123    347 Apr 22  2015 openmp-slurm-shared.sb
```
There are several things to observe with this command:
1. The owner of these new files is the user who ran the commands (username).
2. The use of the `-r` argument is a recursive copy, which gets all files in the directory.
3. The use of the `-p` arguement preserves the date/timestamp, which can be helpful but not always required.
4. The use of one of the special _dot_ characters,  \. in the command above: the syntax tells the operating system to copy all contents of the _/share/apps/examples/OPENMP/_ directory to the `.` directory, or the current directory, which in this case is:

```java
[username@login02 expanse-examples]$ pwd
/home/username/expanse-examples
[username@login02 expanse-examples]$ ls -al  
total 48
drwxr-xr-x 3 username abc123   4 Jul 17 20:32 .
drwxr-x--- 8 username abc123  24 Jul 17 20:20 ..
-rw-r--r-- 1 username abc123 247 Jul 17 20:24 hello_openmp.f90
drwxr-xr-x 2 username abc123   8 Jul 17 20:26 OPENMP
[username@login02 expanse-examples]$ ls -al .
total 48
drwxr-xr-x 3 username abc123   4 Jul 17 20:32 .
drwxr-x--- 8 username abc123  24 Jul 17 20:20 ..
-rw-r--r-- 1 username abc123 247 Jul 17 20:24 hello_openmp.f90
drwxr-xr-x 2 username abc123   8 Jul 17 20:26 OPENMP
```
You can also copy a file or directory and give it a new name:
```
[username@login02 expanse-examples]$  cp -r -p /share/apps/examples/OPENMP/ FOOBAR  
[username@login02 expanse-examples]$ ll
total 49
drwxr-xr-x 4 username abc123   5 Jul 17 21:19 .
drwxr-x--- 9 username abc123  26 Jul 17 21:04 ..
-rw-r--r-- 1 username abc123 247 Jul 17 20:24 hello_openmp.f90
drwxrwxr-x 2 username abc123   8 Mar 12 08:54 OPENMP
drwxrwxr-x 2 username abc123   8 Mar 12 08:54 FOOBAR
[username@login02 expanse-examples]$ ll FOOBAR
total 488
drwxrwxr-x 2 username abc123      8 Mar 12 08:54 .
drwxr-xr-x 4 username abc123      5 Jul 17 21:19 ..
-rwxr-xr-x 1 username abc123 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 username abc123    984 Apr 15  2015 hello_openmp.500005.expanse-27-01.out
-rw-r--r-- 1 username abc123    247 Apr 15  2015 hello_openmp.f90
-rw-r--r-- 1 username abc123    656 Apr 22  2015 hello_openmp_shared.508392.expanse-11-01.out
-rw-r--r-- 1 username abc123    310 Apr 15  2015 openmp-slurm.sb
-rw-r--r-- 1 username abc123    347 Apr 22  2015 openmp-slurm-shared.sb
```
You can rename a directory using the `mv` command:
```
[username@login02 expanse-examples]$ mv FOOBAR/ OPENMP_DUP
[username@login02 expanse-examples]$ /bin/ls -l
total 48
-rw-r--r-- 1 username abc123 247 Jul 17 20:24 hello_openmp.f90
drwxrwxr-x 2 username abc123   8 Mar 12 08:54 OPENMP
drwxrwxr-x 2 username abc123   8 Mar 12 08:54 OPENMP_DUP
[username@login02 expanse-examples]$
```

To move to the directory, use the `cd` (change directory)
```
[username@login02 expanse-examples]$ pwd
/home/username/expanse-examples
[username@login02 expanse-examples]$ cd OPENMP/
[username@login02 OPENMP]$ pwd
/home/username/expanse-examples/OPENMP
[username@login02 OPENMP]$ ls -al
total 479
drwxr-xr-x 2 username abc123      8 Jul 17 20:26 .
drwxr-xr-x 3 username abc123      4 Jul 17 20:32 ..
-rwxr-xr-x 1 username abc123 728112 Jul 17 20:26 hello_openmp
-rw-r--r-- 1 username abc123    984 Jul 17 20:26 hello_openmp.500005.expanse-27-01.out
-rw-r--r-- 1 username abc123    247 Jul 17 20:26 hello_openmp.f90
-rw-r--r-- 1 username abc123    656 Jul 17 20:26 hello_openmp_shared.508392.expanse-11-01.out
-rw-r--r-- 1 username abc123    310 Jul 17 20:26 openmp-slurm.sb
-rw-r--r-- 1 username abc123    347 Jul 17 20:26 openmp-slurm-shared.sb
```
You can sort the order of the file listings by date (or size or other fields -- see the `man` pages). The default file listing in alphabetic, to  see the files in chronological order (or reverse):
```
[username@login02 expanse-examples]$ ls -alt OPENMP/
total 479
drwxr-xr-x 4 username abc123      5 Jul 17 20:43 ..
drwxrwxr-x 2 username abc123      8 Mar 12 08:54 .
-rw-r--r-- 1 username abc123    656 Apr 22  2015 hello_openmp_shared.508392.expanse-11-01.out
-rw-r--r-- 1 username abc123    347 Apr 22  2015 openmp-slurm-shared.sb
-rw-r--r-- 1 username abc123    984 Apr 15  2015 hello_openmp.500005.expanse-27-01.out
-rwxr-xr-x 1 username abc123 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 username abc123    247 Apr 15  2015 hello_openmp.f90
-rw-r--r-- 1 username abc123    310 Apr 15  2015 openmp-slurm.sb

[username@login02 expanse-examples]$ ls -altr OPENMP/
total 479
-rw-r--r-- 1 username abc123    310 Apr 15  2015 openmp-slurm.sb
-rw-r--r-- 1 username abc123    247 Apr 15  2015 hello_openmp.f90
-rwxr-xr-x 1 username abc123 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 username abc123    984 Apr 15  2015 hello_openmp.500005.expanse-27-01.out
-rw-r--r-- 1 username abc123    347 Apr 22  2015 openmp-slurm-shared.sb
-rw-r--r-- 1 username abc123    656 Apr 22  2015 hello_openmp_shared.508392.expanse-11-01.out
drwxrwxr-x 2 username abc123      8 Mar 12 08:54 .
drwxr-xr-x 4 username abc123      5 Jul 17 20:43 ..
```

[Back to Top](#top)
<hr>

## <a name="files">Manipulating Files</a>

This section will show you more ways to manipulate files: copying, listing, deleting and renaming, and examining contents
In the section above, we created files using the `touch` commmand, which will create a file with no contents. First we'll return to the first `testdir` using the `full directory path`:
```
[username@login01 testdir2]$ cd /home/username/testdir
[username@login02 testdir]$ touch myfile1.txt
[username@login02 testdir]$ touch myfile2.txt
[username@login02 testdir]$ ls -l
total 21
drwxr-xr-x 2 username abc123  4 Jul 17 20:53 .
drwxr-x--- 9 username abc123 25 Jul 17 20:49 ..
-rw-r--r-- 1 username abc123  0 Jul 17 20:53 myfile1.txt
-rw-r--r-- 1 username abc123  0 Jul 17 20:53 myfile2.txt
```

To copy a file from another directory  to the current directory, use the full path. In this example, we will copy the _filelisting.txt_ file from the directory above, using the `..` (\"dot-dot\") variable for the directory location:

```java
[username@login02 testdir]$ cp ../filelisting.txt .
[username@login02 testdir]$ ls -l
total 11
-rw-r--r-- 1 username abc123 322 Jul 17 21:09 filelisting.txt
-rw-r--r-- 1 username abc123    0 Jul 17 20:53 myfile1.txt
-rw-r--r-- 1 username abc123    0 Jul 17 20:53 myfile2.txt
```

To rename a file, use the `mv` (move) command:

```java
[username@login02 testdir]$ mv myfile2.txt newfile.txt
[username@login02 testdir]$ ls -l
total 11
-rw-r--r-- 1 username abc123 1543 Jul 17 21:09 filelisting.txt
-rw-r--r-- 1 username abc123    0 Jul 17 20:53 myfile1.txt
-rw-r--r-- 1 username abc123    0 Jul 17 20:53 newfile.txt
```
To delete a file, use the `rm` (remove command):

```
[username@login02 testdir]$ rm myfile1.txt
[username@login02 testdir]$  ls -l
total 10
-rw-r--r-- 1 username abc123 1543 Jul 17 21:09 filelisting.txt
-rw-r--r-- 1 username abc123    0 Jul 17 20:53 newfile.txt
-rw-r--r-- 1 username use300 1410 Jan 18 00:00 sdsc.txt
```
You can examine the contents of a file by using several Linux commands. First, we'll create a small file for testing:
```
[username@login01 testdir]$ ls -al > dirlist.txt
[username@login01 testdir]$ ls -al
total 88
drwxr-xr-x  2 username use300   5 Jan 17 23:49 .
drwxr-x--- 51 username use300  93 Jan 17 23:46 ..
-rw-r--r--  1 username use300 284 Jan 17 23:49 dirlist.txt
-rw-r--r--  1 username use300 322 Jan 17 23:42 filelisting.txt
-rw-r--r--  1 username use300   0 Jan 17 23:42 newfile.txt
-rw-r--r-- 1 username use300 1410 Jan 18 00:00 sdsc.txt
```

To print out the contents of the entire file, use the `cat` command (cat - concatenate files and print on the standard output):
```
[username@login01 testdir]$ cat sdsc.txt
The San Diego Supercomputer Center (SDSC) was established as one of the nation’s first supercomputer centers under a cooperative agreement by the National Science Foundation (NSF) in collaboration with UC San Diego and General Atomics (GA) Technologies. SDSC first opened its doors on November 14, 1985.

For more than 35 years, it has grown and stewarded its national reputation as a pioneer and leader in high-performance and data-intensive computing and cyberinfrastructure. Located on the campus of UC San Diego, SDSC provides resources, services and expertise to the national research community including industry and academia.

Cyberinfrastructure refers to an accessible, integrated network of computer-based resources and expertise, focused on accelerating scientific inquiry and discovery. With Voyager and Expanse, SDSC’s latest supercomputing resources, the center supports hundreds of multidisciplinary programs spanning a wide range of science themes—from earth sciences and biology to astrophysics, bioinformatics and health IT.

SDSC participates in Advanced Cyberinfrastructure Coordination Ecosystem: Services & Support (ACCESS) and was a partner in eXtreme Science and Engineering Discovery Environment (XSEDE), two of the most advanced collections of integrated digital resources and services in the world.

For general inquiries and comments: info@sdsc.edu
SDSC website: www.sdsc.edu

```
The contents of a file may be too large to see at one time, to see how large it is we can run the `wc`, word count command:
```
[username@login01 testdir]$ wc ../README.md 
  644  4531 30519 ../README.md
```
The output says that README file has 644 lines, 4531 words, and 30519 characters.
We might want to look at the beginning (head) or end (tail):
```
[username@login01 testdir]$ head -n 1 sdsc.txt 
The San Diego Supercomputer Center (SDSC) was established as one of the nation’s first supercomputer centers under a cooperative agreement by the National Science Foundation (NSF) in collaboration with UC San Diego and General Atomics (GA) Technologies. SDSC first opened its doors on November 14, 1985.
[username@login01 testdir]$
[username@login01 testdir]$ tail -n 2 sdsc.txt 
For general inquiries and comments: info@sdsc.edu
SDSC website: www.sdsc.edu
```

You can reorder the contents of a file using the `sort` command:
```
[mthomas@login01 testdir]$ sort sdsc.txt
Cyberinfrastructure refers to an accessible, integrated network of computer-based resources and expertise, focused on accelerating scientific inquiry and discovery. With Voyager and Expanse, SDSC’s latest supercomputing resources, the center supports hundreds of multidisciplinary programs spanning a wide range of science themes—from earth sciences and biology to astrophysics, bioinformatics and health IT.
For general inquiries and comments: info@sdsc.edu
For more than 35 years, it has grown and stewarded its national reputation as a pioneer and leader in high-performance and data-intensive computing and cyberinfrastructure. Located on the campus of UC San Diego, SDSC provides resources, services and expertise to the national research community including industry and academia.
SDSC participates in Advanced Cyberinfrastructure Coordination Ecosystem: Services & Support (ACCESS) and was a partner in eXtreme Science and Engineering Discovery Environment (XSEDE), two of the most advanced collections of integrated digital resources and services in the world.
SDSC website: www.sdsc.edu
The San Diego Supercomputer Center (SDSC) was established as one of the nation’s first supercomputer centers under a cooperative agreement by the National Science Foundation (NSF) in collaboration with UC San Diego and General Atomics (GA) Technologies. SDSC first opened its doors on November 14, 1985.
```
The `sort` command is useful for sorting through a long file and reording data.

To search a file for a string you can use the `grep` command:

```
[mthomas@login01 testdir]$ grep -ni SDSC sdsc.txt 
1:The San Diego Supercomputer Center (SDSC) was established as one of the nation’s first supercomputer centers under a cooperative agreement by the National Science Foundation (NSF) in collaboration with UC San Diego and General Atomics (GA) Technologies. SDSC first opened its doors on November 14, 1985.
3:For more than 35 years, it has grown and stewarded its national reputation as a pioneer and leader in high-performance and data-intensive computing and cyberinfrastructure. Located on the campus of UC San Diego, SDSC provides resources, services and expertise to the national research community including industry and academia.
5:Cyberinfrastructure refers to an accessible, integrated network of computer-based resources and expertise, focused on accelerating scientific inquiry and discovery. With Voyager and Expanse, SDSC’s latest supercomputing resources, the center supports hundreds of multidisciplinary programs spanning a wide range of science themes—from earth sciences and biology to astrophysics, bioinformatics and health IT.
7:SDSC participates in Advanced Cyberinfrastructure Coordination Ecosystem: Services & Support (ACCESS) and was a partner in eXtreme Science and Engineering Discovery Environment (XSEDE), two of the most advanced collections of integrated digital resources and services in the world.
9:For general inquiries and comments: info@sdsc.edu
10:SDSC website: www.sdsc.edu
```
In the command above, we used the `grep -ni` argument to get the line number, and to ignore case. 

[Back to Top](#top)
<hr>



## <a name="permissions">Permissions</a>
In the section we will look breifly at how to set file permissions. Before you can change the file permissions, you need to own it or have permission as a 2023 member. For a more detailed tutorial, see http://www.nersc.gov/users/storage-and-file-systems/unix-file-permissions/. Permissions are written in the first column, with fields that specify whether or not the file is a directory (`d`), what the read/write/execution permissions (`rwx`) for the files are for users and groups.  Using the example below:

```
[username@login02 OPENMP]$ ls -l hello_openmp
total 479
drwxr-xr-x 2 username abc123      2 Jul 17 21:53 direxample
-rwxr-xr-x 1 username abc123 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 username abc123    247 Apr 15  2015 hello_openmp.f90
```
The order of the markers are grouped into 4 fields:
`-` `rwx` `r-x` `r-x`
Field 1 == directory, a `d` or `-` means directory or not a directory
Field 2 == owner permissions 'rwx' means the owner can read, write, and exectute
Field 3 == 2023 permissions 'rwx' means the owner can read and exectute, but not modify
Field 4 == other/world permissions 'r-x' means the others can read and exectute, but not modiry

To change the file access permissions, use the `chmod` command. In the example below, only user username has permission to edit (`rw-`) the files, members of the 2023 abc123 and others have read only permission (`--`). There are several ways to modify permissions, we will use the binary representation where the rwx status represents a binary number 2^n, where n is the position of the permission starting from the right. For example:
```
  r-- = 2^2 + 0 + 0 = 4 + 0 + 0 = 4
  rw- = 2^2 + 2^1 + 0 = 4 + 2 + 0 = 6
  r-x = 2^2 + 0 + 2^0 = 4 + 0 + 1 = 5
  rwx = 2^2 + 2^1 + 2^0 = 4 + 2 + 1 = 7
```

In the example below, we will set read and write permissions to the owner and the group, and limit the other/world 2023 to read only:
```
[username@login02 OPENMP]$ ls -l
total 479
drwxr-xr-x 2 username abc123      2 Jul 17 21:53 direxample
-rwxr-xr-x 1 username abc123 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 username abc123    984 Apr 15  2015 hello_openmp.500005.expanse-27-01.out
-rw-r--r-- 1 username abc123    247 Apr 15  2015 hello_openmp.f90
-rw-r--r-- 1 username abc123    656 Apr 22  2015 hello_openmp_shared.508392.expanse-11-01.out
-rw-r--r-- 1 username abc123    310 Apr 15  2015 openmp-slurm.sb
-rw-r--r-- 1 username abc123    347 Apr 22  2015 openmp-slurm-shared.sb
[username@login02 OPENMP]$ chmod 660 *
[username@login02 OPENMP]$ ls -l
total 460
drwxr-xr-x 2 username abc123      2 Jul 17 21:53 direxample
-rw-rw-r-- 1 username abc123 728112 Apr 15  2015 hello_openmp
-rw-rw---- 1 username abc123    984 Apr 15  2015 hello_openmp.500005.expanse-27-01.out
-rw-rw---- 1 username abc123    247 Apr 15  2015 hello_openmp.f90
-rw-rw---- 1 username abc123    656 Apr 22  2015 hello_openmp_shared.508392.expanse-11-01.out
-rw-rw---- 1 username abc123    310 Apr 15  2015 openmp-slurm.sb
-rw-rw---- 1 username abc123    347 Apr 22  2015 openmp-slurm-shared.sb

```
In the example above, we use the star wildcard, \" \* \" to represent all the files in the directory (See the section on wildcards below). We can use the wildcard to **change the group** of some of the files. For example, to change the 2023 of only the \*.out files:

```
[username@login02 OPENMP]$ groups
abc123 pet heart scicom-docs grdclus webwrt ...
[username@login02 OPENMP]$ chgrp heart *.out
[username@login02 OPENMP]$ ls -l
total 460
drwxr-xr-x 2 username abc123      2 Jul 17 21:53 direxample
-rw-rw-r-- 1 username abc123 728112 Apr 15  2015 hello_openmp
-rw-rw---- 1 username heart     984 Apr 15  2015 hello_openmp.500005.expanse-27-01.out
-rw-rw---- 1 username abc123    247 Apr 15  2015 hello_openmp.f90
-rw-rw---- 1 username heart     656 Apr 22  2015 hello_openmp_shared.508392.expanse-11-01.out
-rw-rw---- 1 username abc123    310 Apr 15  2015 openmp-slurm.sb
-rw-rw---- 1 username abc123    347 Apr 22  2015 openmp-slurm-shared.sb
```

[Back to Top](#top)
<hr>

## <a name="wildcards">Wildcards</a>

\"A wildcard is a character that can be used as a substitute for any of a class of characters in a search, thereby greatly increasing the flexibility and efficiency of searches."  The wildcards are very powerful, and there is not room in this document for all of them, so we recommend that you check out this site:  http://www.linfo.org/wildcard.html for more information.

In the example below, we use the star wildcard to list all files ending in `.out`

```
[username@login02 OPENMP]$ ls -al *.out
-rw-rw---- 1 username heart 984 Apr 15  2015 hello_openmp.500005.expanse-27-01.out
-rw-rw---- 1 username heart 656 Apr 22  2015 hello_openmp_shared.508392.expanse-11-01.out
```

[Back to Top](#top)
<hr>

## <a name="common-utilities">Other Utilities to Learj: </a>
* grep,  sort, tar, gzip ,and pigz

