### Intro

This is a quick and dirty readme for development. Better, production-quality
readme coming soon.

#### Overview

This set of ansible plays will setup a (TODO: name?) device.

#### Initialization

Initialization should be done the first time you setup a (TODO: name) device
box.

Run the `init` script. This will create the following directories:
   * `hosts`: stores ansible inventory files
   * `keys`: stores deployment SSH keys
   * `vars`: stores playbook variables (e.g. root password) in ansible-vault
     format

`init` will also randomly generate a root and deploy password and store them
in `vars/secrets.yml` (encrypted with ansible-vault). Finally, `init` creates
an ed25519 SSH keypair and drops it into keys.

#### Usage

After initialization, just run:
```
ansible-playbook -i hosts/hostfile bootstrap-playbook.yml
```
to run the playbook.

*NOTE*: a hostfile is purposefully left unspecified to try to help avoid
accidentally running the bootstrap playbook on an established (TODO: name?)
device. The `-i` argument manually specifies an inventory file to use.
