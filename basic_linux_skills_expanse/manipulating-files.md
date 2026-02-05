---
title: "Manipulating Files"
sidebar_position: 4
---

### Overview

This section will show you more ways to manipulate files: copying, listing, deleting and renaming, and examining contents

---

### Creating files with `touch`

In the section above, we created files using the `touch` commmand, which will create a file with no contents. First we'll return to the first `testdir` using the `full directory path`:

```sh
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

---

### Copying files with `cp`

To copy a file from another directory  to the current directory, use the full path. In this example, we will copy the _filelisting.txt_ file from the directory above, using the `..` ("dot-dot") variable for the directory location:

```sh
[username@login02 testdir]$ cp ../filelisting.txt .
[username@login02 testdir]$ ls -l
total 11
-rw-r--r-- 1 username abc123 322 Jul 17 21:09 filelisting.txt
-rw-r--r-- 1 username abc123    0 Jul 17 20:53 myfile1.txt
-rw-r--r-- 1 username abc123    0 Jul 17 20:53 myfile2.txt
```

---

### Renaming files with `mv`

To rename a file, use the `mv` (move) command:

```sh
[username@login02 testdir]$ mv myfile2.txt newfile.txt
[username@login02 testdir]$ ls -l
total 11
-rw-r--r-- 1 username abc123 1543 Jul 17 21:09 filelisting.txt
-rw-r--r-- 1 username abc123    0 Jul 17 20:53 myfile1.txt
-rw-r--r-- 1 username abc123    0 Jul 17 20:53 newfile.txt
```

---

### Deleting files with `rm`

To delete a file, use the `rm` (remove command):

```sh
[username@login02 testdir]$ rm myfile1.txt
[username@login02 testdir]$  ls -l
total 10
-rw-r--r-- 1 username abc123 1543 Jul 17 21:09 filelisting.txt
-rw-r--r-- 1 username abc123    0 Jul 17 20:53 newfile.txt
-rw-r--r-- 1 username use300 1410 Jan 18 00:00 sdsc.txt
```

---

### Examining file contents

You can examine the contents of a file by using several Linux commands. First, we'll create a small file for testing:

```sh
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

```sh
[username@login01 testdir]$ cat sdsc.txt
The San Diego Supercomputer Center (SDSC) was established as one of the nation’s first supercomputer centers under a cooperative agreement by the National Science Foundation (NSF) in collaboration with UC San Diego and General Atomics (GA) Technologies. SDSC first opened its doors on November 14, 1985.

For more than 35 years, it has grown and stewarded its national reputation as a pioneer and leader in high-performance and data-intensive computing and cyberinfrastructure. Located on the campus of UC San Diego, SDSC provides resources, services and expertise to the national research community including industry and academia.

Cyberinfrastructure refers to an accessible, integrated network of computer-based resources and expertise, focused on accelerating scientific inquiry and discovery. With Voyager and Expanse, SDSC’s latest supercomputing resources, the center supports hundreds of multidisciplinary programs spanning a wide range of science themes—from earth sciences and biology to astrophysics, bioinformatics and health IT.

SDSC participates in Advanced Cyberinfrastructure Coordination Ecosystem: Services & Support (ACCESS) and was a partner in eXtreme Science and Engineering Discovery Environment (XSEDE), two of the most advanced collections of integrated digital resources and services in the world.

For general inquiries and comments: info@sdsc.edu
SDSC website: www.sdsc.edu

```

:::note
The contents of a file may be too large to see at one time, to see how large it is we can run the `wc`, word count command:
:::

```sh
[username@login01 testdir]$ wc ../README.md 
  644  4531 30519 ../README.md
```

The output says that README file has 644 lines, 4531 words, and 30519 characters.  
We might want to look at the beginning (head) or end (tail):

```sh
[username@login01 testdir]$ head -n 1 sdsc.txt 
The San Diego Supercomputer Center (SDSC) was established as one of the nation’s first supercomputer centers under a cooperative agreement by the National Science Foundation (NSF) in collaboration with UC San Diego and General Atomics (GA) Technologies. SDSC first opened its doors on November 14, 1985.
[username@login01 testdir]$
[username@login01 testdir]$ tail -n 2 sdsc.txt 
For general inquiries and comments: info@sdsc.edu
SDSC website: www.sdsc.edu
```

---

### Sorting and searching file contents

You can reorder the contents of a file using the `sort` command:

```sh
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

```sh
[mthomas@login01 testdir]$ grep -ni SDSC sdsc.txt 
1:The San Diego Supercomputer Center (SDSC) was established as one of the nation’s first supercomputer centers under a cooperative agreement by the National Science Foundation (NSF) in collaboration with UC San Diego and General Atomics (GA) Technologies. SDSC first opened its doors on November 14, 1985.
3:For more than 35 years, it has grown and stewarded its national reputation as a pioneer and leader in high-performance and data-intensive computing and cyberinfrastructure. Located on the campus of UC San Diego, SDSC provides resources, services and expertise to the national research community including industry and academia.
5:Cyberinfrastructure refers to an accessible, integrated network of computer-based resources and expertise, focused on accelerating scientific inquiry and discovery. With Voyager and Expanse, SDSC’s latest supercomputing resources, the center supports hundreds of multidisciplinary programs spanning a wide range of science themes—from earth sciences and biology to astrophysics, bioinformatics and health IT.
7:SDSC participates in Advanced Cyberinfrastructure Coordination Ecosystem: Services & Support (ACCESS) and was a partner in eXtreme Science and Engineering Discovery Environment (XSEDE), two of the most advanced collections of integrated digital resources and services in the world.
9:For general inquiries and comments: info@sdsc.edu
10:SDSC website: www.sdsc.edu
```

In the command above, we used the `grep -ni` argument to get the line number, and to ignore case. 

---

[Back to Top](#top)
