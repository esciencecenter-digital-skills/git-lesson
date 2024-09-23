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

#### Install Shell and Git. 
   
:::tab

### Windows
Git should be installed on your computer as part of your Bash install.


### Mac  
Mac

### Linux
If Git is not already available on your machine you can install it via your distro's package manager. Debian/Ubuntu run 'sudo apt-get install git' and for Fedora run 'sudo dnf install git'.

:::
  
#### Setup GitHub 

You will need an account for [GitHub](https://github.com/) to follow episodes 7, 8, 9 in this lesson.

1. To sign up for an account, navigate to https://github.com/ and follow the prompts.
2. Verify your email address.
3. Configure GitHub authentication.

You must authenticate before you can access certain resources on GitHub.
Each way of accessing GitHub supports different authentication method. For example, you can authenticate with GitHub via the command line using Secure Shell Protocol (SSH) or you can authenticate with GitHub via browser using two-factor authentication (2FA). In our lesson we shall use both.

:::tab

### SSH   

To set up SSH for your GitHub account, follow these steps:

1. Generate an SSH public/private keypair on your local machine if you don't already have one.

To check your local machine for existing SSH keys, run the following command in the terminal:

```bash
    ls -al ~/.ssh
```

Then check the directory listing to see if you already have a public SSH key. By default, the filenames of supported public keys for GitHub are one of the following.

```bash
    id_rsa.pub
    id_ecdsa.pub
    id_ed25519.pub
```

If you receive an error that ~/.ssh does not exist, you do not have an existing SSH key pair in the default location. You can create a new SSH key pair in the next step. If you do have an existing SSH key pair, you can skip the next step.

2. Generate a new SSH key.

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
When you're prompted to "Enter a file in which to save the key", you can press Enter to accept the default file location. 

3. Add your SSH key to the ssh-agent.

```bash
# Start the ssh-agent in the background
eval "$(ssh-agent -s)"
# Add your SSH private key to the ssh-agent
ssh-add ~/.ssh/id_ed25519
```

4. Add SSH Key to GitHub Account

Finally, you need to add your SSH key to your GitHub account. To do this, you need to copy the SSH key to your clipboard. You can do this by running the following command:

```bash     
cat ~/.ssh/id_ed25519.pub
```

Then, copy the output to your clipboard. Next, navigate to your GitHub account settings, and click on SSH and GPG keys. Click on the New SSH key button, and paste your key into the Key field. Click Add SSH key to add your key to your GitHub account.

### 2FA 

To set up 2FA for your GitHub account, follow these steps:

1. If you already use an authenticator app, like [Google Authenticator](https://support.google.com/accounts/answer/1066447?hl=en&co=GENIE.Platform%3DiOS&oco=0) on your smartphone for example, add GitHub to that app.
2. If you have access to a smartphone but do not already use an authenticator app, install one and add GitHub to the app.
3. Optionally, you can add a passkey to your account. Passkeys are similar to security keys. However, passkeys satisfy both password and 2FA requirements, so you can sign in to your account in one step.

:::

Refer to the GitHub [documentation](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github) for more details about authentication.


#### Confirm that everything works

You should now be able to open a terminal window and execute the following commands:

#### Git

```bash
$ git --version
```
which will return (something similar to):

```bash
git version 2.34.1
```

#### Github accreturningount & SSH connection

```bash
ssh git@github.com
```

which will return:

```bashreturning
Hi [username]! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```

### If something does not work

Follow the corresponding setup instructions. If you still need help, send us an [email](training@esciencecenter.nl).
