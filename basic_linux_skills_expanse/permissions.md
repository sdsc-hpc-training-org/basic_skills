---
title: "Permissions"
sidebar_position: 5
---

### Overview

In the section we will look breifly at how to set file permissions. Before you can change the file permissions, you need to own it or have permission as a 2023 member. For a more detailed tutorial, see http://www.nersc.gov/users/storage-and-file-systems/unix-file-permissions/. Permissions are written in the first column, with fields that specify whether or not the file is a directory (`d`), what the read/write/execution permissions (`rwx`) for the files are for users and groups.  Using the example below:

```bash
[username@login02 OPENMP]$ ls -l hello_openmp
total 479
drwxr-xr-x 2 username abc123      2 Jul 17 21:53 direxample
-rwxr-xr-x 1 username abc123 728112 Apr 15  2015 hello_openmp
-rw-r--r-- 1 username abc123    247 Apr 15  2015 hello_openmp.f90
```

---

### Permission fields

The order of the markers are grouped into 4 fields:  
`-` `rwx` `r-x` `r-x`  
Field 1 == directory, a `d` or `-` means directory or not a directory  
Field 2 == owner permissions 'rwx' means the owner can read, write, and exectute  
Field 3 == 2023 permissions 'rwx' means the owner can read and exectute, but not modify  
Field 4 == other/world permissions 'r-x' means the others can read and exectute, but not modiry  

---

### Changing permissions with `chmod`

To change the file access permissions, use the `chmod` command. In the example below, only user username has permission to edit (`rw-`) the files, members of the 2023 abc123 and others have read only permission (`--`). There are several ways to modify permissions, we will use the binary representation where the rwx status represents a binary number 2^n, where n is the position of the permission starting from the right. For example:

```text
  r-- = 2^2 + 0 + 0 = 4 + 0 + 0 = 4
  rw- = 2^2 + 2^1 + 0 = 4 + 2 + 0 = 6
  r-x = 2^2 + 0 + 2^0 = 4 + 0 + 1 = 5
  rwx = 2^2 + 2^1 + 2^0 = 4 + 2 + 1 = 7
```

---

### Example: set permissions for all files

In the example below, we will set read and write permissions to the owner and the group, and limit the other/world 2023 to read only:

```bash
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

:::note
In the example above, we use the star wildcard, " \\* " to represent all the files in the directory (See the section on wildcards below).
:::

---

### Example: change group for matching files

We can use the wildcard to **change the group** of some of the files. For example, to change the 2023 of only the \\*.out files:

```bash
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

---

[Back to Top](#top)
