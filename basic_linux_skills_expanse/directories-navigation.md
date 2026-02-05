---
title: "Directories and Navigation"
sidebar_position: 2
---

### Directories and the current location

In unix, everything is a file, which can be confusing at first. The locations for where files are stored are called directories (which is equivalent to folders), and are also viewed as files by the operating system. To find out where you are in the system, use the `pwd` command (print working directory), which prints the full path to the directory you are currently in:

```sh
[username@login02 ~]$ pwd
/home/username
```

---

### Listing directory contents

To see what are the contents of the current directory are, use the file listing command `ls`:

```sh
[username@login02 ~]$ ls
filelisting.txt intel   loadgccomgnuenv.sh  loadgnuenv.sh	loadintelenv.sh  tools
```

In every Unix directory, there are "hidden" files (just like on Macs and Windows machines), to see them, run the `ls -a` command:

```sh
[username@login02 ~]$ ls -a
.	.bash_history  .bashrc	 .gitconfig  loadgccomgnuenv.sh  .ncviewrc     .ssh	 .vimrc
..	.bash_logout   .config filelisting.txt	 intel	     loadgnuenv.sh	 .petscconfig  tools	 .Xauthority
.alias	.bash_profile    .kshrc      loadintelenv.sh	 .slurm        .viminfo
```

---

### File details and permissions

In Unix, sometimes it is hard tell if a file is a directory. To see file details (including timestamp and size), run the `ls -l` command:

```sh
[username@login02 ~]$ ls -l
-rw-r--r-- 1 username abc123 322 Jul 17 21:04 filelisting.txt
drwxr-xr-x 3 username abc123   3 Jun 22  2023 intel
-rwx------ 1 username abc123 101 Jun 27  2023 loadgccomgnuenv.sh
-rwx------ 1 username abc123  77 Oct 16  2023 loadgnuenv.sh
-rwxr-xr-x 1 username abc123 125 Oct 16  2023 loadintelenv.sh
drwxr-xr-x 2 username abc123   4 Jun 30  2023 tools
```

You can combine the two commands above and use it to see the full directory and file information:

```sh
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

:::note
There are several things to notice in the above listing: the first column of data is information about the file "permissions", which controls who can see/read/modify what files (`r`=read, `w`=write, `x`=execute, `-`=no permission); the next 2 columns are the username and groupID; the 3rd and 4th columns are the size and date. This is discussed in more detail in the [Permissions](#permissions) section below. Also, note that two files have `dots` for their names: in unix the "dot" is a component of a filename. When working with filenames, a leading dot is the prefix of a "hidden" file, a file that an `ls` will not normally show. But also, the single dot, `.` represents the current working directory, and the double dots, `..` represent the directory above. You use these as arguments to unix commands dealing with directories.
:::

---

### Creating and navigating directories

There are simple Linux commands to create and remove directories, and to populate the directories.  
To create a directory, use the `mkdir`, make directory command (more about directories in the sections below):

```sh
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

```sh
[username@login02 ~]$ cd testdir/
[username@login02 testdir]$ ls -al
total 20
drwxr-xr-x 2 username abc123  2 Jul 17 20:49 .
drwxr-x--- 9 username abc123 25 Jul 17 20:49 ..
[username@login02 testdir]$
```

From this directory, you can use the `..` command to see the contents of the directory above:

```sh
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

---

### Removing files and directories

To remove files and directories there are different mechanisms, depending on whether or not the directory is empty or contains files.

```sh
[username@login01 testdir]$ cd ..
[username@login01 testdir]$ mkdir testdir2
[username@login01 testdir]$ cd testdir2
[username@login01 testdir2]$ mkdir dir1
[username@login01 testdir2]$ mkdir dir2
[username@login01 testdir2]$ mkdir dir3
```

Next, create some testfiles using the `touch` command:

```sh
[username@login01 testdir2]$ touch f1
[username@login01 testdir2]$ touch f2
[username@login01 testdir2]$ touch f3
[username@login01 testdir2]$ touch dir2/file1
[username@login01 testdir2]$ touch dir2/file2
[username@login01 testdir2]$ touch dir2/file3
```

For a file, we use the remove, `rm` command:

```sh
[username@login01 testdir2]$ rm f3
```

For an *empty* directory, we can use the `rmdir` command:

```sh
[username@login01 testdir2]$ rmdir dir1
```

:::warning
If the directory has contents (files or subdirectories), you use the `rm` command with arguments to *force* the removal of the directory and all of its contents.
:::

```sh
[username@login01 testdir2]$ rm -rf dir3
```

---

[Back to Top](#top)
