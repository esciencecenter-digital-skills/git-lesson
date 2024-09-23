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
   
::: tab

### Windows
Git should be installed on your computer as part of your Bash install.


### Mac  
Mac

### Linux
If Git is not already available on your machine you can install it via your distro's package manager. For Go to https://github.com and follow the “Sign up” link at the top-right of the window.
Follow the instructions to create an account.
Verify your email address with GitHub.
Configure multifactor authentication (see below).Debian/Ubuntu run sudo apt-get install git and for Fedora run sudo dnf install git.

:::
  
#### Create a GitHub account. 

You will need an account for [GitHub](https://github.com/) to follow episodes 7, 8, 9 in this lesson.

1. To sign up for an account, navigate to https://github.com/ and follow the prompts.
2. Verify your email address.
3. Configure two-factor authentication.
   
Two-factor authentication, or 2FA, is an extra layer of security used when logging into websites or apps. It is strongly adviced to configure 2FA.
The steps are summarised below:

1. If you already use an authenticator app, like [Google Authenticator](https://support.google.com/accounts/answer/1066447?hl=en&co=GENIE.Platform%3DiOS&oco=0) on your smartphone for example, add GitHub to that app.
2. If you have access to a smartphone but do not already use an authenticator app, install one and add GitHub to the app.
3. Optionally, you can add a passkey to your account. Passkeys are similar to security keys. However, passkeys satisfy both password and 2FA requirements, so you can sign in to your account in one step. 

Refer to the GitHub [documentation](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication) for more details about configuring 2FA.

#### Set up an SSH connection to GitHub. 

Please refer to [this page](https://coderefinery.github.io/installation/ssh/) for instructions.

#### Confirm that everything works

You should now be able to open a terminal window and execute the following commands:

#### Git

```bash
$ git --version
```
returning (something similar to):

```bash
git version 2.34.1
```

#### Github account & SSH connection

```bash
ssh git@github.com
```

which will return:training@esciencecenter.nl 

```bash
Hi [username]! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```

### If something does not work

Follow the corresponding setup instructions. If you still need help, send us an [email](training@esciencecenter.nl).
