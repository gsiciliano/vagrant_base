# Vagrant Machine + Ansible provisioning

## Introduction

This repository allows you to setup your own Vagrant machine for local tests as well as provision & deploy the app on a remote server.

>OS: Ubuntu 14.04
>Provisioning: Ansible
>Tested with Vagrant v 1.8 (with local Ansible provisioning)
>Installation procedure has been verified starting from a Linux operating system, **Ubuntu** distro, the command examples are referred to that operating system, in case a different OS is used map the corresponding command or action.
>
>OS: **Windows** 7/8/8.x/10 x86 x86_64

Linux requirements
--------------------

* Install Virtualbox:

    `sudo apt-get install virtualbox`

* Install Vagrant:

    `sudo apt-get install vagrant` 

* Install NFS:

    `sudo apt-get install nfs-kernel-server nfs-common portmap`

* Install Git        

    `sudo apt-get install git`

* Install vagrant-hostmanager plugin
                
     On Ubuntu 16.04 there are a couple of prerequisites in order to be able to install the Vagrant plugin:
        `sudo apt-get install zlib1g-dev`
                 
>    _On Ubuntu 16.04 you will need to patch Ruby in order to make it work, check this question and follow the steps provided for the solution: [http://stackoverflow.com/questions/36811863/cant-install-vagrant-plugins-in-ubuntu-16-04](http://stackoverflow.com/questions/36811863/cant-install-vagrant-plugins-in-ubuntu-16-04)_                 

Windows requirements
------------------------

* Download and install virtualbox (https://www.virtualbox.org)
* Download and install vagrant (https://www.vagrantup.com)
* Download cygwin (http://www.cygwin.com)
+ Install following cygwin modules:
    * binutils
    * curl
    * gmp
    * libgmp-devel
    * make
    * python (2.7.x)
    * python-crypto
    * python-openssl
    * python-setuptools
    * git (2.5.x)
    * nano
    * openssh
    * openssl
    * openssl-devel

> _if windows 8.x or 10: right-click on cigwin.bat -> properties -> advanced: thick "Run as administrator"_

* From cygwin terminal Install Ansible:
    
    `easy_install-2.7 pip`
    
    `pip install ansible`
                
Installation and provision
----------------------------

* In your working directory clone the required repositories
    
    `git clone https://bitbucket.org/zanichelli/vagrant_base`

* Create ssh key (with name id_rsa_vagrant) if needed:
    
    `ssh-keygen -t rsa`
    
    `cp id_rsa_vagrant.pub <repo_directory>/roles/webserver_provision/files/public-keys/.`

* Go in the directory where you cloned the **vagrant_base** repository and start the machine provisioning from there. then wait until it completes.

    `run vagrant up --provision`
    
    The command provisions and starts the machine.

To start/stop machine
------------------------
* To start the machine: `vagrant up` (use `--provision` if you need to verify the machine is up to date with the latest infrastructure and configuration changes)

* To stop the machine: `vagrant halt`

Notes
-------

The ip address of your machine is: **172.16.16.16**

When code is modified on the cloned repositories on the host machine, the virtual machine see automatically those changes because it maps those dirs.

Adding deploy configurations
------------------------------

Feel free to add deploy configuration for your projects adding ansible tasks to playbook.yml.

To run ansible for deploy apps use:

`ansible-playbook playbook.yml -i inventory/<server-inventory> -t "deploy-<appname>-app" -v`
    
in cygwin terminal from Windows or shell terminal in Linux    