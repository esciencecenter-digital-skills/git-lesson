---
title: Setup
---

::::::::::::::::::::::::::::::prereq

In this lesson we use Git from the Unix Shell. Some previous experience with the shell is expected, but isn’t mandatory.

::::::::::::::::::::::::::::::

## Computer

Participants must work on a computer with a Mac, Linux, or Windows operating system (not a tablet, Chromebook, etc.) on which they have administrative privileges.

## Software Setup

To participate in this workshop, you will need to prepare the following (if you haven't already):

1. Install Shell and Git. 
   
::: tab

### Windows
Git should be installed on your computer as part of your Bash install.


### Mac  
Mac

### Linux
If Git is not already available on your machine you can install it via your distro's package manager. For Debian/Ubuntu run sudo apt-get install git and for Fedora run sudo dnf install git.

:::

1. Create a GitHub account. Please refer to [this page](https://coderefinery.github.io/installation/github/) for instructions.
2. Set up an SSH connection to GitHub. Please refer to [this page](https://coderefinery.github.io/installation/ssh/) for instructions.

### To confirm that everything works

You should now be able to open a terminal window and execute the following commands:

#### Git

```bash
$ git --version
```
returning (something similar to):

```bash
git version 2.34.1https://github.com/swcarpentry/git-novice/blob/main/learners/setup.md
```

#### Github account & SSH connection

```bash
ssh git@github.com
```

which will return:

```bash
Hi [username]! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```

### If something does not work

Follow the corresponding setup instructions. If you still need help, send us an email at training@esciencecenter.nl.
