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
IPPROOT=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/ipp
INTEL_LICENSE_FILE=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/licenses:/opt/intel/licenses:/root/intel/licenses
L_MKL_TEMP=M_VERS
TERM=xterm-256color
SHELL=/bin/bash
HISTSIZE=5000
GDBSERVER_MIC=/opt/intel/2018.1.163/debugger_YEAR/gdb/targets/mic/bin/gdbserver
SSH_CLIENT=76.176.117.51 58136 22
CONDA_SHLVL=1
LIBRARY_PATH=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/compiler/lib/intel64_lin:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/ipp/../compiler/lib/intel64:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/ipp/lib/intel64:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/mkl/lib/intel64:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/tbb/lib/intel64/gcc4.4
CONDA_PROMPT_MODIFIER=(base) 
FPATH=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/mkl/include
QTDIR=/usr/lib64/qt-3.3
QTINC=/usr/lib64/qt-3.3/include
MIC_LD_LIBRARY_PATH=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/compiler/lib/mic:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/mkl/lib/mic:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/tbb/lib/mic
ROCKSROOT=/opt/rocks/share/devel
SSH_TTY=/dev/pts/103
ANT_HOME=/opt/rocks
QT_GRAPHICSSYSTEM_CHECKED=1
USER=mthomas
LD_LIBRARY_PATH=/opt/mvapich2/intel/ib/lib:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/compiler/lib/intel64_lin:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/ipp/../compiler/lib/intel64:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/ipp/lib/intel64:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/mkl/lib/intel64:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/tbb/lib/intel64/gcc4.4
LS_COLORS=rs=0:di=38;5;27:ln=38;5;51:mh=44;38;5;15:pi=40;38;5;11:so=38;5;13:do=38;5;5:bd=48;5;232;38;5;11:cd=48;5;232;38;5;3:or=48;5;232;38;5;9:mi=05;48;5;232;38;5;15:su=48;5;196;38;5;15:sg=48;5;11;38;5;16:ca=48;5;196;38;5;226:tw=48;5;10;38;5;16:ow=48;5;10;38;5;21:st=48;5;21;38;5;15:ex=38;5;34:*.tar=38;5;9:*.tgz=38;5;9:*.arc=38;5;9:*.arj=38;5;9:*.taz=38;5;9:*.lha=38;5;9:*.lz4=38;5;9:*.lzh=38;5;9:*.lzma=38;5;9:*.tlz=38;5;9:*.txz=38;5;9:*.tzo=38;5;9:*.t7z=38;5;9:*.zip=38;5;9:*.z=38;5;9:*.Z=38;5;9:*.dz=38;5;9:*.gz=38;5;9:*.lrz=38;5;9:*.lz=38;5;9:*.lzo=38;5;9:*.xz=38;5;9:*.bz2=38;5;9:*.bz=38;5;9:*.tbz=38;5;9:*.tbz2=38;5;9:*.tz=38;5;9:*.deb=38;5;9:*.rpm=38;5;9:*.jar=38;5;9:*.war=38;5;9:*.ear=38;5;9:*.sar=38;5;9:*.rar=38;5;9:*.alz=38;5;9:*.ace=38;5;9:*.zoo=38;5;9:*.cpio=38;5;9:*.7z=38;5;9:*.rz=38;5;9:*.cab=38;5;9:*.jpg=38;5;13:*.jpeg=38;5;13:*.gif=38;5;13:*.bmp=38;5;13:*.pbm=38;5;13:*.pgm=38;5;13:*.ppm=38;5;13:*.tga=38;5;13:*.xbm=38;5;13:*.xpm=38;5;13:*.tif=38;5;13:*.tiff=38;5;13:*.png=38;5;13:*.svg=38;5;13:*.svgz=38;5;13:*.mng=38;5;13:*.pcx=38;5;13:*.mov=38;5;13:*.mpg=38;5;13:*.mpeg=38;5;13:*.m2v=38;5;13:*.mkv=38;5;13:*.webm=38;5;13:*.ogm=38;5;13:*.mp4=38;5;13:*.m4v=38;5;13:*.mp4v=38;5;13:*.vob=38;5;13:*.qt=38;5;13:*.nuv=38;5;13:*.wmv=38;5;13:*.asf=38;5;13:*.rm=38;5;13:*.rmvb=38;5;13:*.flc=38;5;13:*.avi=38;5;13:*.fli=38;5;13:*.flv=38;5;13:*.gl=38;5;13:*.dl=38;5;13:*.xcf=38;5;13:*.xwd=38;5;13:*.yuv=38;5;13:*.cgm=38;5;13:*.emf=38;5;13:*.axv=38;5;13:*.anx=38;5;13:*.ogv=38;5;13:*.ogx=38;5;13:*.aac=38;5;45:*.au=38;5;45:*.flac=38;5;45:*.mid=38;5;45:*.midi=38;5;45:*.mka=38;5;45:*.mp3=38;5;45:*.mpc=38;5;45:*.ogg=38;5;45:*.ra=38;5;45:*.wav=38;5;45:*.axa=38;5;45:*.oga=38;5;45:*.spx=38;5;45:*.xspf=38;5;45:
CONDA_EXE=/home/mthomas/miniconda3/bin/conda
MIC_LIBRARY_PATH=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/compiler/lib/mic:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/tbb/lib/mic
ROCKS_ROOT=/opt/rocks
CPATH=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/ipp/include:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/mkl/include:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/tbb/include
_CE_CONDA=
NLSPATH=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/compiler/lib/intel64_lin/locale/%l_%t/%N:/opt/intel/2018.1.163/debugger_YEAR/gdb/intel64/share/locale/%l_%t/%N
MV2_ALLTOALL_TUNING=2
MAIL=/var/spool/mail/mthomas
PATH=/home/mthomas/miniconda3/bin:/home/mthomas/miniconda3/condabin:/opt/mvapich2/intel/ib/bin:/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/bin/intel64:/usr/lib64/qt-3.3/bin:/usr/local/bin:/bin:/usr/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/opt/sdsc/bin:/opt/sdsc/sbin:/opt/ibutils/bin:/opt/pdsh/bin:/opt/rocks/bin:/opt/rocks/sbin:/home/mthomas/bin
SDSCDEVEL=/opt/sdsc/devel
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
SDSCHOME=/opt/sdsc
CONDA_PYTHON_EXE=/home/mthomas/miniconda3/bin/python
PYTHONPATH=/opt/sdsc/lib
LOGNAME=mthomas
QTLIB=/usr/lib64/qt-3.3/lib
CVS_RSH=ssh
XDG_DATA_DIRS=/home/mthomas/.local/share/flatpak/exports/share:/var/lib/flatpak/exports/share:/usr/local/share:/usr/share
SSH_CONNECTION=76.176.117.51 58136 198.202.113.253 22
MODULESHOME=/usr/share/Modules
CONDA_DEFAULT_ENV=base
MKL_ROOT=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/mkl
LESSOPEN=||/usr/bin/lesspipe.sh %s
INFOPATH=/opt/intel/2018.1.163/documentation_YEAR/en/debugger/gdb-ia/info/:/opt/intel/2018.1.163/documentation_YEAR/en/debugger/gdb-mic/info
XDG_RUNTIME_DIR=/run/user/15294
INCLUDE=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux/mkl/include
INTELHOME=/opt/intel/2018.1.163/compilers_and_libraries_2018.1.163/linux
BASH_FUNC_module()=() {  eval `/usr/bin/modulecmd bash $*`
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
XXXXXXXXXXXXXXX
Copies of files and directories use the same command: `cp`. 
For a large number of files, it is easier to copy the entire directory using the `-R` or `-r` recursive command:
```
[mthomas@comet-ln2 comet-examples]$ cp -r -p /share/apps/examples/OPENMP/ .
[mthomas@comet-ln2 comet-examples]$ ll
total 48
drwxr-xr-x 3 mthomas use300   4 Jul 17 20:26 .
drwxr-x--- 8 mthomas use300  24 Jul 17 20:20 ..
-rw-r--r-- 1 mthomas use300 247 Jul 17 20:24 hello_openmp.f90
drwxr-xr-x 2 mthomas use300   8 Jul 17 20:26 OPENMP
[mthomas@comet-ln2 comet-examples]$ ls -al OPENMP/
total 479
drwxrwxr-x 2 mthomas use300      8 Mar 12 08:54 .
drwxr-xr-x 3 mthomas use300      4 Jul 17 20:32 ..
-rwxr-xr-x 1 mthomas use300 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 mthomas use300    984 Apr 15  2015 hello_openmp.500005.comet-27-01.out
-rw-r--r-- 1 mthomas use300    247 Apr 15  2015 hello_openmp.f90
-rw-r--r-- 1 mthomas use300    656 Apr 22  2015 hello_openmp_shared.508392.comet-11-01.out
-rw-r--r-- 1 mthomas use300    310 Apr 15  2015 openmp-slurm.sb
-rw-r--r-- 1 mthomas use300    347 Apr 22  2015 openmp-slurm-shared.sb
```
There are several things to observe with this command:
1. The owner of these new files is the user who ran the commands (mthomas).
2. The use of the `-r` argument is a recursive copy, which gets all files in the directory.
3. The use of the `-p` arguement preserves the date/timestamp, which can be helpful but not always required.
4. The use of one of the special _dot_ characters,  \. in the command above: the syntax tells the operating system to copy all contents of the _/share/apps/examples/OPENMP/_ directory to the `.` directory, or the current directory, which in this case is:

```java
[mthomas@comet-ln2 comet-examples]$ pwd
/home/mthomas/comet-examples
[mthomas@comet-ln2 comet-examples]$ ls -al  
total 48
drwxr-xr-x 3 mthomas use300   4 Jul 17 20:32 .
drwxr-x--- 8 mthomas use300  24 Jul 17 20:20 ..
-rw-r--r-- 1 mthomas use300 247 Jul 17 20:24 hello_openmp.f90
drwxr-xr-x 2 mthomas use300   8 Jul 17 20:26 OPENMP
[mthomas@comet-ln2 comet-examples]$ ls -al .
total 48
drwxr-xr-x 3 mthomas use300   4 Jul 17 20:32 .
drwxr-x--- 8 mthomas use300  24 Jul 17 20:20 ..
-rw-r--r-- 1 mthomas use300 247 Jul 17 20:24 hello_openmp.f90
drwxr-xr-x 2 mthomas use300   8 Jul 17 20:26 OPENMP
```
You can also copy a file or directory and give it a new name:
```
[mthomas@comet-ln2 comet-examples]$  cp -r -p /share/apps/examples/OPENMP/ FOOBAR  
[mthomas@comet-ln2 comet-examples]$ ll
total 49
drwxr-xr-x 4 mthomas use300   5 Jul 17 21:19 .
drwxr-x--- 9 mthomas use300  26 Jul 17 21:04 ..
-rw-r--r-- 1 mthomas use300 247 Jul 17 20:24 hello_openmp.f90
drwxrwxr-x 2 mthomas use300   8 Mar 12 08:54 OPENMP
drwxrwxr-x 2 mthomas use300   8 Mar 12 08:54 FOOBAR
[mthomas@comet-ln2 comet-examples]$ ll FOOBAR
total 488
drwxrwxr-x 2 mthomas use300      8 Mar 12 08:54 .
drwxr-xr-x 4 mthomas use300      5 Jul 17 21:19 ..
-rwxr-xr-x 1 mthomas use300 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 mthomas use300    984 Apr 15  2015 hello_openmp.500005.comet-27-01.out
-rw-r--r-- 1 mthomas use300    247 Apr 15  2015 hello_openmp.f90
-rw-r--r-- 1 mthomas use300    656 Apr 22  2015 hello_openmp_shared.508392.comet-11-01.out
-rw-r--r-- 1 mthomas use300    310 Apr 15  2015 openmp-slurm.sb
-rw-r--r-- 1 mthomas use300    347 Apr 22  2015 openmp-slurm-shared.sb
```
You can rename a directory using the `mv` command:
```
[mthomas@comet-ln2 comet-examples]$ mv FOOBAR/ OPENMP_DUP
[mthomas@comet-ln2 comet-examples]$ /bin/ls -l
total 48
-rw-r--r-- 1 mthomas use300 247 Jul 17 20:24 hello_openmp.f90
drwxrwxr-x 2 mthomas use300   8 Mar 12 08:54 OPENMP
drwxrwxr-x 2 mthomas use300   8 Mar 12 08:54 OPENMP_DUP
[mthomas@comet-ln2 comet-examples]$
```

To move to the directory, use the `cd` (change directory)
```
[mthomas@comet-ln2 comet-examples]$ pwd
/home/mthomas/comet-examples
[mthomas@comet-ln2 comet-examples]$ cd OPENMP/
[mthomas@comet-ln2 OPENMP]$ pwd
/home/mthomas/comet-examples/OPENMP
[mthomas@comet-ln2 OPENMP]$ ls -al
total 479
drwxr-xr-x 2 mthomas use300      8 Jul 17 20:26 .
drwxr-xr-x 3 mthomas use300      4 Jul 17 20:32 ..
-rwxr-xr-x 1 mthomas use300 728112 Jul 17 20:26 hello_openmp
-rw-r--r-- 1 mthomas use300    984 Jul 17 20:26 hello_openmp.500005.comet-27-01.out
-rw-r--r-- 1 mthomas use300    247 Jul 17 20:26 hello_openmp.f90
-rw-r--r-- 1 mthomas use300    656 Jul 17 20:26 hello_openmp_shared.508392.comet-11-01.out
-rw-r--r-- 1 mthomas use300    310 Jul 17 20:26 openmp-slurm.sb
-rw-r--r-- 1 mthomas use300    347 Jul 17 20:26 openmp-slurm-shared.sb
```
You can sort the order of the file listings by date (or size or other fields -- see the `man` pages). The default file listing in alphabetic, to  see the files in chronological order (or reverse):
```
[mthomas@comet-ln2 comet-examples]$ ls -alt OPENMP/
total 479
drwxr-xr-x 4 mthomas use300      5 Jul 17 20:43 ..
drwxrwxr-x 2 mthomas use300      8 Mar 12 08:54 .
-rw-r--r-- 1 mthomas use300    656 Apr 22  2015 hello_openmp_shared.508392.comet-11-01.out
-rw-r--r-- 1 mthomas use300    347 Apr 22  2015 openmp-slurm-shared.sb
-rw-r--r-- 1 mthomas use300    984 Apr 15  2015 hello_openmp.500005.comet-27-01.out
-rwxr-xr-x 1 mthomas use300 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 mthomas use300    247 Apr 15  2015 hello_openmp.f90
-rw-r--r-- 1 mthomas use300    310 Apr 15  2015 openmp-slurm.sb

[mthomas@comet-ln2 comet-examples]$ ls -altr OPENMP/
total 479
-rw-r--r-- 1 mthomas use300    310 Apr 15  2015 openmp-slurm.sb
-rw-r--r-- 1 mthomas use300    247 Apr 15  2015 hello_openmp.f90
-rwxr-xr-x 1 mthomas use300 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 mthomas use300    984 Apr 15  2015 hello_openmp.500005.comet-27-01.out
-rw-r--r-- 1 mthomas use300    347 Apr 22  2015 openmp-slurm-shared.sb
-rw-r--r-- 1 mthomas use300    656 Apr 22  2015 hello_openmp_shared.508392.comet-11-01.out
drwxrwxr-x 2 mthomas use300      8 Mar 12 08:54 .
drwxr-xr-x 4 mthomas use300      5 Jul 17 20:43 ..
```

[Back to Top](#top)
<hr>

## <a name="permissions">Permissions</a>
In the section we will look breifly at how to file permissions. Before you can change the file permissions, you need to own it or have permission as a group member. For a more detailed tutorial, see http://www.nersc.gov/users/storage-and-file-systems/unix-file-permissions/. Permissions are written in the first column, with fields that specify whether or not the file is a directory (`d`), what the read/write/execution permissions (`rwx`) for the files are for users and groups.  Using the example below:

```
[mthomas@comet-ln2 OPENMP]$ ls -l hello_openmp
total 479
drwxr-xr-x 2 mthomas use300      2 Jul 17 21:53 direxample
-rwxr-xr-x 1 mthomas use300 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 mthomas use300    247 Apr 15  2015 hello_openmp.f90
```
The order of the markers are grouped into 4 fields:
`-` `rwx` `r-x` `r-x`
Field 1 == directory, a `d` or `-` means directory or not a directory
Field 2 == owner permissions 'rwx' means the owner can read, write, and exectute
Field 3 == group permissions 'rwx' means the owner can read and exectute, but not modify
Field 4 == other/world permissions 'r-x' means the others can read and exectute, but not modiry

To change the file access permissions, use the `chmod` command. In the example below, only user mthomas has permission to edit (`rw-`) the files, members of the group use300 and others have read only permission (`--`). There are several ways to modify permissions, we will use the binary representation where the rwx status represents a binary number 2^n, where n is the position of the permission starting from the right. For example:
```
  r-- = 2^2 + 0 + 0 = 4 + 0 + 0 = 4
  rw- = 2^2 + 2^1 + 0 = 4 + 2 + 0 = 6
  r-x = 2^2 + 0 + 2^0 = 4 + 0 + 1 = 5
  rwx = 2^2 + 2^1 + 2^0 = 4 + 2 + 1 = 7
```

In the example below, we will set read and write permissions to the owner and the group, and limit the other/world group to read only:
```
[mthomas@comet-ln2 OPENMP]$ ls -l
total 479
drwxr-xr-x 2 mthomas use300      2 Jul 17 21:53 direxample
-rwxr-xr-x 1 mthomas use300 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 mthomas use300    984 Apr 15  2015 hello_openmp.500005.comet-27-01.out
-rw-r--r-- 1 mthomas use300    247 Apr 15  2015 hello_openmp.f90
-rw-r--r-- 1 mthomas use300    656 Apr 22  2015 hello_openmp_shared.508392.comet-11-01.out
-rw-r--r-- 1 mthomas use300    310 Apr 15  2015 openmp-slurm.sb
-rw-r--r-- 1 mthomas use300    347 Apr 22  2015 openmp-slurm-shared.sb
[mthomas@comet-ln2 OPENMP]$ chmod 660 *
[mthomas@comet-ln2 OPENMP]$ ls -l
total 460
drwxr-xr-x 2 mthomas use300      2 Jul 17 21:53 direxample
-rw-rw-r-- 1 mthomas use300 728112 Apr 15  2015 hello_openmp
-rw-rw---- 1 mthomas use300    984 Apr 15  2015 hello_openmp.500005.comet-27-01.out
-rw-rw---- 1 mthomas use300    247 Apr 15  2015 hello_openmp.f90
-rw-rw---- 1 mthomas use300    656 Apr 22  2015 hello_openmp_shared.508392.comet-11-01.out
-rw-rw---- 1 mthomas use300    310 Apr 15  2015 openmp-slurm.sb
-rw-rw---- 1 mthomas use300    347 Apr 22  2015 openmp-slurm-shared.sb

```
In the example above, we use the star wildcard, \" \* \" to represent all the files in the directory (See the section on wildcards below). We can use the wildcard to **change the group** of some of the files. For example, to change the group of only the \*.out files:

```
[mthomas@comet-ln2 OPENMP]$ groups
use300 pet heart scicom-docs grdclus webwrt ...
[mthomas@comet-ln2 OPENMP]$ chgrp heart *.out
[mthomas@comet-ln2 OPENMP]$ ls -l
total 460
drwxr-xr-x 2 mthomas use300      2 Jul 17 21:53 direxample
-rw-rw-r-- 1 mthomas use300 728112 Apr 15  2015 hello_openmp
-rw-rw---- 1 mthomas heart     984 Apr 15  2015 hello_openmp.500005.comet-27-01.out
-rw-rw---- 1 mthomas use300    247 Apr 15  2015 hello_openmp.f90
-rw-rw---- 1 mthomas heart     656 Apr 22  2015 hello_openmp_shared.508392.comet-11-01.out
-rw-rw---- 1 mthomas use300    310 Apr 15  2015 openmp-slurm.sb
-rw-rw---- 1 mthomas use300    347 Apr 22  2015 openmp-slurm-shared.sb
```

[Back to Top](#top)
<hr>

## <a name="wildcards">Wildcards</a>

\"A wildcard is a character that can be used as a substitute for any of a class of characters in a search, thereby greatly increasing the flexibility and efficiency of searches."  The wildcards are very powerful, and there is not room in this document for all of them, so we recommend that you check out this site:  http://www.linfo.org/wildcard.html for more information.

In the example below, we use the star wildcard to list all files ending in `.out`

```
[mthomas@comet-ln2 OPENMP]$ ls -al *.out
-rw-rw---- 1 mthomas heart 984 Apr 15  2015 hello_openmp.500005.comet-27-01.out
-rw-rw---- 1 mthomas heart 656 Apr 22  2015 hello_openmp_shared.508392.comet-11-01.out
```
 
[Back to Top](#top)
<hr>

## <a name="common-utilities">Common Utilities</a>
 common utilities: grep, cat, less, head, sort, tar, gzip ,and pigz
