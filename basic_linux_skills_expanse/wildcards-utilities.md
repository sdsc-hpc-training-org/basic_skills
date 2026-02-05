---
title: "Wildcards and Utilities"
sidebar_position: 6
---

# Wildcards

### Overview

"A wildcard is a character that can be used as a substitute for any of a class of characters in a search, thereby greatly increasing the flexibility and efficiency of searches." The wildcards are very powerful, and there is not room in this document for all of them, so we recommend that you check out this site: http://www.linfo.org/wildcard.html for more information.

---

### Using the `*` wildcard

In the example below, we use the star wildcard to list all files ending in `.out`

```bash
[username@login02 OPENMP]$ ls -al *.out
-rw-rw---- 1 username heart 984 Apr 15  2015 hello_openmp.500005.expanse-27-01.out
-rw-rw---- 1 username heart 656 Apr 22  2015 hello_openmp_shared.508392.expanse-11-01.out
```

:::note
The `*` wildcard matches **zero or more characters**, making it useful for working with groups of files that share a common naming pattern.
:::

---

## Other Utilities to Learn

The following utilities are commonly used when working with files and directories:

- `grep`
- `sort`
- `tar`
- `gzip`
- `pigz`

---

[Back to Top](#top)
