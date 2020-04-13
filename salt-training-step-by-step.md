# SALT Training Step-by-step Guide

This guide is intended to be used in conjunction with the SALT training course
by users participating in the training.

Goals for training:
* Successfully deploy a SALT minion
* Successfully deploy fireeye to a SALT minion

## Pre-requisites

* Git installed on local machine
* GitHub account provisioned and 2FA setup
* SSH key created and public key stored in GitHub
* Repository cloned to local machine
* Azure labs virtual machine started and accessible
* PSA account provisioned and 2FA setup

### Git installation

Git will need to be installed on your local machine. Git is available for 
download for Mac OS X, Windows, and Linux/Unix platforms:

https://git-scm.com/downloads

### GitHub provisioning

Verify that you can sign into GitHub with your primary account:

https://github.gatech.edu/

Enable 2FA:

https://github.gatech.edu/settings/security

Once setup is complete, verify access to the SALT repository:

https://github.gatech.edu/delegated-admin/gt-salt-oit

### SSH key maintenance

Run the following command in a termainl window (or Git Bash) to create an SSH
key:

```
ssh-keygen -t rsa
```

Once successful, two files will be created: `id_rsa` and `id_rsa.pub`. Upload the
contents of the `id_rsa.pub` to GitHub:

https://github.gatech.edu/settings/ssh/new

### Cloning the repository

Clone the repository to your local machine, create a local working branch, and
push your branch to GitHub.

```
git clone git@github.gatech.edu:delegated-admin/gt-salt-oit.git
git checkout -b <primary-account>
git push -u origin <primary-account>
```

### Azure labs VM

For testing and development, we will be using an Azure labs virtual machine to
act as our minion.

Start your virtual machine:

https://labs.azure.com/virtualmachines

Once your VM is started, you will be given an SSH command to connect. It will
look similar to the following:

```
ssh -p 51283 train@ml-lab-472b6307-8340-49f2-9b37-cdbc831fb8e7.eastus.cloudapp.azure.com
```

Run the SSH command in a terminal to connect to your VM. The first time that you
connect to your VM, please reset the resolv.conf file:

```
cd ~/
sudo ./reset-resolv-conf.sh
```

## Setting up the SALT minion

Connect to your Azure labs VM and install the SALT minion:

```
sudo curl https://sse.salt.gatech.edu/bootstrap/enroll | sudo bash -s "<branch-name>" "ai-trn-m01.salt.gatech.edu"

```

Add your ID (id: \<primary-account\>) to the end of the minion's configuration file. Please note that the space following the colon is required.

```
sudo vim /etc/salt/minion.d/minion.conf
```

TODO: add diff here with id line syntax.

After adding the ID, restart the SALT minion:

```
sudo systemctl restart salt-minion
```

## Deploy chrony

SALT comes prepackaged with default configuration setups for common apps. Here
will walk through the steps necessary to deploy chrony to a SALT minion.

```
salt-call state.apply chrony
```
