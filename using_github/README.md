# Using GitHub at SDSC

Github repositories can be accessed and updated on all SDSC HPC systems. 
Make sure your local system or laptop can run git. 

## Suggested On-line Tutorials

* [https://swcarpentry.github.io/git-novice/](https://swcarpentry.github.io/git-novice/)


<a name="top">**Contents::**
* [Create Git Account](#git-acct)
* [Install Git on Local System](#git-install)
* [Install Git on Linux](#git-install-linux)
* [Install Git on Mac](#git-install-mac)
* [Install Git on Windows](#git-install-windows)
* [Clone the Git repository](#git-clone)
* [Checkout a branch](#git-branch)


## Create a GitHub Account: <a name="git-acct"></a>
* See:  see https://github.com/join 
* If you do not currently have a [GitHub](https://github.com/) account, you must obtain one prior to attending the SDSC training activities.
* Working with  `git` and GitHub will be covered in both introductory and advanced training sessions on these tools.

## Install Git on Local System <a name="git-install"></a>

* To learn the basics of setting up GitHub, see this guide:  [https://help.github.com/en/articles/set-up-git](https://help.github.com/en/articles/set-up-git). 

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

### Installing `git` on Windows:

* There are also several ways to install `git` under Windows. The official binary executable is available for download on the `git` website is here:

[https://git-scm.com/download/win](https://git-scm.com/download/win)

* If you've chosen to work on the [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about)
 follow the installation directions for Linux given above.

## Cloning a Repository:<a name="git-clone"></a>

* GitHub supports two ways to clone a repository: (1) Anonymous HTTPS cloning (no account required);  (2) Authenticated method using a SSH, which requires authentication to a GitHub account associated with the repository.
* As an example, we will download the SDSC Jupyter "Notebook Examples" Repository:
  * [https://github.com/sdsc-hpc-training-org/notebook-examples](https://github.com/sdsc-hpc-training-org/notebook-examples)

* Anonymous HTTPS Method: click on the option on the GitHub repo

* To clone the Notebook repository:
  * Open a terminal window on your laptop. Optionally, create a directory to save the repo; cd into that directory
  * In your browser, open the link to the repository web page: [https://github.com/sdsc-hpc-training-org/notebook-examples](https://github.com/sdsc-hpc-training-org/notebook-examples)
  * Click on the green "Clone or Download" and select the "Clone with HTTPS" option
  * copy the  repository link in the box
  * In your terminal window, type the following command
```
$ git clone https://github.com/sdsc-hpc-training-org/notebook-examples.git
```

* The repository should start downloading in the directory from which you ran the ```clone``` command.

* Authenticated cloning:  This method requires that you create a [GitHub](https://github.com/) account and then you must be added to the repository project team. 

## Checkout a Branch:<a name="git-branch"></a>

* Make sure you have the main repository cloned locally. Then change to the root of the local repository.

```
(base) [username@login01 ~]$ git clone https://github.com/sdsc-hpc-training-org/basic_skills.git
Cloning into 'basic_skills'...
remote: Enumerating objects: 330, done.
remote: Counting objects: 100% (330/330), done.
remote: Compressing objects: 100% (240/240), done.
remote: Total 330 (delta 152), reused 160 (delta 58), pack-reused 0
Receiving objects: 100% (330/330), 4.10 MiB | 12.21 MiB/s, done.
Resolving deltas: 100% (152/152), done.
(base) [username@login01 ~]$ cd basic_skills/
```
* List all available branches:

```
(base) [username@login01 basic_skills]$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/basic_skills_branch
  remotes/origin/master   
```

* Notice that it lists both the branches that are local and the remote branches on Bitbucket. Using the list as reference, choose the branch you want to checkout.  In this example, we want ```basic_skills_branch.```

```
(base) [username@login01 basic_skills]$ git checkout basic_skills_branch
Branch 'basic_skills_branch' set up to track remote branch 'basic_skills_branch' from 'origin'.
Switched to a new branch 'basic_skills_branch'
(base) [username@login01 basic_skills]$ 
(base) [username@login01 basic_skills]$ 
```

* Verify that you have checkout the right branch:

```
(base) [username@login01 basic_skills]$ 
(base) [username@login01 basic_skills]$ git branch

* basic_skills_branch
  master
(base) [username@login01 basic_skills]$ 
```

* At this point, all changes made will affect the branch, not the master
