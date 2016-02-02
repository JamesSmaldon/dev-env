# Development Environment Setup

## Requirements
Virtualbox 5.0.14
Vagrant 1.8.1

## To login to VM from putty on Windows
Putty can't load the private key created by vagrant without conversion to 
.ppk format, to do this open the following private key file in puttygen:

```
.vagrant\machines\default\virtualbox\private_key
```
Then save it as key.ppk in the dev-env directory. You can then setup putty 
to use the private key file and login to vagrant@localhost:2222.

## Fixing redraw issues with 3D acceleration
In the end I had to install the mate desktop manager
```
sudo apt-get install mint-meta-mate
```

Then go into control centre->Desktop Setting->Windows and select compiz, then 
click reset compiz settings.

Then install the compiz settings manager, and go to utility, and enable the 
redraw fixes.

## Refs
- [Using ansible galaxy](https://servercheck.in/blog/using-ansible-galaxy)
- [ansible-vagrant-examples](https://github.com/geerlingguy/ansible-vagrant-examples)
