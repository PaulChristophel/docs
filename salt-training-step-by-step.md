# SALT Training Step-by-step Guide

This guide is intended to be used in conjunction with the SALT training course
by users participating in the training.

## Pre-requisites

* Git installed on local machine
* GitHub account provisioned and 2FA setup
* SSH key created and public key stored in GitHub
* Azure labs virtual machine started and accessible
* PSA account provisioned and 2FA setup

### Git installation

Git is available for download for Mac OS X, Windows, and Linux/Unix platforms:

https://git-scm.com/downloads

### GitHub provisioning

Verify that you can sign into GitHub with your primary account:

https://github.gatech.edu/

Enable 2FA:

https://github.gatech.edu/settings/security

Once setup is complete, verify access to the SALT repo:

https://github.gatech.edu/delegated-admin/gt-salt-oit

### SSH key maintenance

1. Open a terminal.
2. Run the following command:

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

