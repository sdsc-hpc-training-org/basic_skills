---
title: Install Git on Local System
position: 2
---

:::note
* To learn the basics of setting up GitHub, see this guide:  
  [https://help.github.com/en/articles/set-up-git](https://help.github.com/en/articles/set-up-git).
:::

### Install `git` on Linux:<a name="git-install-linux"></a>

If you want to install `git` on a Linux-based operating system, you should be
able to do so via your operating system's standard package management tool. For
example, on any RPM-based Linux distribution, such as Fedora, RHEL, or CentOS, 
you can use `dnf`:

```
$ sudo dnf install git-all
```

Or on any Debian-based distribution, such as Ubuntu, try `apt`:

```
$ sudo apt install git-all
```

---

### Installing `git` on Mac OS X:

There are several ways to install `git` on your Mac. However, probably the 
easiest way is to install the [Xcode](https://developer.apple.com/xcode/) 
Command Line Tools, which you should be able to do by simply tying to run git 
from your [Terminal](https://support.apple.com/guide/terminal/welcome/mac):

```
$ git --version
```

If it's not already installed, you should be prompted to install it.

If the above option does not work or you need a more up-to-date version of 
`git`, you can always install it via a binary installer maintained by the `git`
team, which is available for download at: 

[https://git-scm.com/download/mac](https://git-scm.com/download/mac). 

The download should start immediately.

---

### Installing `git` on Windows:

:::tip
* There are also several ways to install `git` under Windows. The official binary executable is available for download on the `git` website is here:
[Git Window Download](https://git-scm.com/download/win)
:::

* If you've chosen to work on the [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about)
 follow the installation directions for Linux given above.
