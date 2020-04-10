# SALT Training Step-by-step Guide

This guide is intended to be used in conjunction with the SALT training course
by users in the training.

## Pre-requisites

* Git setup on local machine
* GitHub account provisioned and accessible
* GitHub account granted access to `gt-salt-oit` repository
* SSH key created and public key stored in GitHub
* Azure labs virtual machine provisioned and accessible

### SSH key creation

1. Open a terminal window.
  1. If a windows user, please open Git Bash as the terminal.
1. Run the following command:

```
ssh-keygen -t rsa
```

  1. Enter a passphrase (twice).

### SSH key upload to GitHub

TODO: steps to upload the ssh key to github.

## Cloning the repository

```
git clone git@github.gatech.edu:delegated-admin/gt-salt-oit.git
git checkout -b <gt-username>
git push -u origin <gt-username>
```

These commands will clone the repository, create a local branch for you to work
in, checkout that branch, and to push your local branch back to GitHub.

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
1. Open the minion configuration file to add your id:
  ```
  sudo vim /etc/salt/miniond./minion.conf
  id: <gt-username>
  sudo systemctl restart salt-minion
  ```

