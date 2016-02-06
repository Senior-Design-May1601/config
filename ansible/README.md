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

#### Vagrant Usage

to Run Vagrant test network hosts file should look something like
[pi]
192.168.42.43
[admin]
192.168.42.42

With this in place one should simply be able to 'vagrant up'  and Vm's should provision themselves.


#### Splunk communication

Once the Admin Vm has been provisioned, user should be able to access the Splunk web service on their host machine at 
192.168.42.42:8000
