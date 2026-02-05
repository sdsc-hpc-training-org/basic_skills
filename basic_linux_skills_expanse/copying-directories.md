---
title: "Copying Directories"
sidebar_position: 3
---

### Overview

A common task in computing is to work with examples and collaborator files. Suppose we want to copy the contents of another directory to our local directory. On Expanse, there is a large suite of applications that you can work with. In this example, we will copy the GPU application folder. Suppose you are interested in working with one of the files or directories in the /share/apps/examples/ directory.

---

### Create a working directory

First, we will make a folder to hold expanse examples and then `cd` into that new directory. This is done using the `mkdir` command:

```sh
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

---

### Look at the example directory

Next, we will look at the directory where the OPENMP code is stored:

```sh
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

---

### Copy a single file

Copies of files and directories use the same command: `cp`. To copy a single file to the `expanse-examples` directory, we need to use the full path:

```sh
[username@login02 expanse-examples]$ cp /share/apps/examples/OPENMP/hello_openmp.f90 hello_openmp.f90
[username@login02 expanse-examples]$ ls -al
total 29
drwxr-xr-x 2 username abc123   3 Jul 17 20:24 .
drwxr-x--- 8 username abc123  24 Jul 17 20:20 ..
-rw-r--r-- 1 username abc123 247 Jul 17 20:24 hello_openmp.f90
```

---

### Copy an entire directory

For a large number of files, it is easier to copy the entire directory using the `-R` or `-r` recursive command:

```sh
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

:::note
There are several things to observe with this command:  
1. The owner of these new files is the user who ran the commands (username).  
2. The use of the `-r` argument is a recursive copy, which gets all files in the directory.  
3. The use of the `-p` arguement preserves the date/timestamp, which can be helpful but not always required.  
4. The use of one of the special _dot_ characters,  \\. in the command above: the syntax tells the operating system to copy all contents of the _/share/apps/examples/OPENMP/_ directory to the `.` directory, or the current directory, which in this case is:
:::

```sh
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

---

### Copy with a new name

You can also copy a file or directory and give it a new name:

```sh
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

---

### Rename a directory

You can rename a directory using the `mv` command:

```sh
[username@login02 expanse-examples]$ mv FOOBAR/ OPENMP_DUP
[username@login02 expanse-examples]$ /bin/ls -l
total 48
-rw-r--r-- 1 username abc123 247 Jul 17 20:24 hello_openmp.f90
drwxrwxr-x 2 username abc123   8 Mar 12 08:54 OPENMP
drwxrwxr-x 2 username abc123   8 Mar 12 08:54 OPENMP_DUP
[username@login02 expanse-examples]$
```

---

### Move into the directory

To move to the directory, use the `cd` (change directory)

```sh
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

---

### Sorting file listings

You can sort the order of the file listings by date (or size or other fields -- see the `man` pages). The default file listing in alphabetic, to  see the files in chronological order (or reverse):

```sh
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

---

[Back to Top](#top)
