# SALT Training Step-by-step Guide

This guide is intended to be used in conjunction with the SALT training course
by users participating in the training.

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
git checkout -b <gt-username>
git push -u origin <gt-username>
```

### Azure labs VM

For testing and development, we will be using an Azure labs virtual machine.

Start your virtual machine:

https://labs.azure.com/virtualmachines

Once your VM is started, you will be given an SSH command to connect. It will
look similar to the following:

```
ssh -p 51283 train@ml-lab-472b6307-8340-49f2-9b37-cdbc831fb8e7.eastus.cloudapp.azure.com
```

Run the SSH command in a terminal to connect to your VM.

## Installing the SALT minion

1. SSH to your provisioned Azure labs VM.
1. Run the resolv.conf reset script:
  ```
  cd ~/
  sudo ./reset-resolv-conf.sh
  ```
1. Install SALT minion from the internal bootstrap site:
  ```
  sudo curl https://sse.salt.gatech.edu/bootstrap/enroll | sudo bash -s "<branch-name>" "ai-trn-m01.salt.gatech.edu"
  ```
1. Edit the minion configuration.
  1. Open the minion configuration
  ```
  sudo vim /etc/salt/miniond./minion.conf
  ```
  1. Add the following lines to the end of the file:
  ```
  id: <gt-username>
  ```
  1. Restart the minion.
  ```
  sudo systemctl restart salt-minion
  ```

