---
title: Using Git at SDSC
position: 3
---


## Cloning a Repository:<a name="git-clone"></a>

:::note
* GitHub supports two ways to clone a repository: (1) Anonymous HTTPS cloning (no account required);  
  (2) Authenticated method using a SSH, which requires authentication to a GitHub account associated with the repository.
:::

* As an example, we will download the SDSC Jupyter "Notebook Examples" Repository:
  * [https://github.com/sdsc-hpc-training-org/notebook-examples](https://github.com/sdsc-hpc-training-org/notebook-examples)

---

### Anonymous HTTPS Method

* Anonymous HTTPS Method: click on the option on the GitHub repo

* To clone the Notebook repository:
  * Open a terminal window on your laptop. Optionally, create a directory to save the repo; cd into that directory
  * In your browser, open the link to the repository web page:  
    [https://github.com/sdsc-hpc-training-org/notebook-examples](https://github.com/sdsc-hpc-training-org/notebook-examples)
  * Click on the green "Clone or Download" and select the "Clone with HTTPS" option
  * copy the repository link in the box
  * In your terminal window, type the following command

```
$ git clone https://github.com/sdsc-hpc-training-org/notebook-examples.git
```

* The repository should start downloading in the directory from which you ran the ```clone``` command.

:::tip
* Authenticated cloning: This method requires that you create a [GitHub](https://github.com/) account and then you must be added to the repository project team.
:::

---

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

:::note
* Notice that it lists both the branches that are local and the remote branches on Bitbucket. Using the list as reference, choose the branch you want to checkout. In this example, we want ```basic_skills_branch.```
:::

```
(base) [username@login01 basic_skills]$ git checkout basic_skills_branch
Branch 'basic_skills_branch' set up to track remote branch 'basic_skills_branch' from 'origin'.
Switched to a new branch 'basic_skills_branch'
(base) [username@login01 basic_skills]$ 
(base) [username@login01 basic_skills]$ 
```

* Verify that you have checkout the right branch:

```
(base) [username@login01 basic_skills]$ git branch

* basic_skills_branch
  master
(base) [username@login01 basic_skills]$ 
```

:::warning
* At this point, all changes made will affect the branch, not the master
:::
