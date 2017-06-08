# Scripting Oracle Public Cloud Depolyments Using Ansible

## Overview

These Ansible scripts illustrate how an Oracle Database and Weblogic server environment can be created on the Oracle Public Cloud. They allow a complete environment to be scripted using the [REST API's of the Oracle Public Cloud](https://apicatalog.oraclecloud.com/ui/)

## Running scripts on Windows
As you may have already read, Ansible manages Linux/Unix machines using SSH by default. There are ways to use if from Windows but the approach I've taken is to create a Virtualbox VM image for the Ansible Control Machine, and run all the commands from there. The instructions below outline how to do this;

### Create a VirtualBox Linux Image using Vagrant

Install Git, Vagrant and Virtualbox and then use git to clone this repository to your laptop. Then opne a Windows shell in the cloned repository directory, where the Vagrantfile is located, run the commnad `vagrant up`. This will cause Vagrant to create a VirtualBox image of a Linux VM with Ansible already installed.

### Login to the new VirtualBox Image (VM) using Vagrant

In the same Windows shell that you called the `vagrant up` command, add Git to the Windows PATH as follows;

`set PATH=%PATH%;C:\Program Files\Git\usr\bin`

Tihs will allow the Vagrant SSH command to work. Then logon to the Lnux VM using the command `vagrant ssh`. The `/vagrant` directory in the Linux VM will contain all these files in the cloned repository, which have been auto mounted. The user you logon/SSH as is vagrant.

BTW if you don't like the colour scheme of the Ansible output, or find it hard to read - as I do, then you can update the "nocolor" setting in the `/etc/ansible/ansible.cfg` file or set the `ANSIBLE_NOCOLOR` environment variable to 1 

## Script Description

The scripts use Ansible Roles to partition the creation of differnet infrastructure components. The tasks used by each role are also designed to be idempotent, so they will teardown any existing installation and recreate it from scratch wehn run. The main Ansible playbook is opc.yaml in the base directory. 

To create an environment first update the configuration parameter file in `vars/all.yaml` and then run the following command in the base (`/vargrant/opc`) directory;

`ansible-playbook create-site.yaml`

This will create an Oracle database and Weblogic server instance on the DBaaS and JCS services. If you want to delete the site you have created then run the command;

`ansible-playbook delete-site.yaml`

Note: for detailed output you can use the `-vvv` option

