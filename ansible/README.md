### Intro

This is a quick and dirty readme for development. Better, production-quality
readme coming soon.

#### Overview

This set of ansible plays will setup a (TODO: name?) device.

#### Dependencies

There are several dependencies necessary to execute these playbooks.
Note that Ansible should be installed using 'pip'.

Make sure the following are installed:
   * Ansible 2.0.1
   * Vagrant 1.8.1
   * Sshpass

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

##Future functionality
'init' will also ask the user for a Splunk auth Token value, an administrative hostname, and an administrative email address to notify when (TODO: name) Honeypots need to be updated

The variables stored in vars/sercrets.yml are encrypted using ansible vault. to decrypt this file, simply run
$ ansible-vault decrypt secrets.yml
and provide your vault pass

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

to Run Vagrant test network hosts file should look like

[pi]
192.168.42.42
[splunk]
192.168.42.43


Where the names and ip addresses of these VM's correspond with the parameters set in the Vagrantfile.

the script Splunk-init script should also be executed to generate the splunk auth certificates and ssh dummy keys. Follow the prompts.

Once you've generated your auth certs copy them into the config directory. 

the following config files should also be created and modified inside config/toml. use the template files included in config/toml as a guide

dnp3-config.toml
fssh-config.toml
main-config.toml
Splunk-config.toml
webauth-config.toml 

##Admin IP Note
inside vars/genvars there is a varaiable for Admin ip. This should be the ip that you are given by virtualbox on this network so shouldn't need to be changed.

Now you should be able to run 
sudo vagrant up

or if you prefer, you can boot up only a single machine by calling it directly
sudo vagrant up pi

Vm are provisioned by default the first time they are booted up, but not after that. to re-provision an existing vm run
sudo vagrant provision pi

initially vagrant uses the user/pass combo vagrant vagrant to ssh into the vm, but it replaces the pass entry with a default vagrant key(i think) and prevents continued log in by just hard coding ssh vagrant@192.168.42.43
Instead,use command
sudo vagrant ssh 


##Reminder
you will need to allow the splunk event collector via the Splunk web interface.
 
##Tags

Ansible tags allow for the user to define which segments of the playbook the wish to run. Tag support has been added on the "play" level, meaning it will allow you to skip large chunks of the playbook if you wish to save time or only need to reprovision a small portion of code. To use the tags via Vagrant, simply edit the vagrant file and remove the tags corresponding to plays you don't wish to run insde the quotes which should look something like
ansible.tags="sysconfig,install,build,serviceConfig,serviceStart"

unfortunately, vagrant does not support command line entry of specific tags to run, unlike ansible.


#### Splunk communication

Once the Splunk Vm has been provisioned, user should be able to access the Splunk web service on their host machine at 
192.168.42.42:8000
