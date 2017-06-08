# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "centos/7"
  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"
  config.vm.box_check_update = true
  config.vm.provision "shell", inline: <<-SHELL
    yum -y install epel-release
    yum -y install ansible
    yum -y install wget
  SHELL
	  
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false 
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end

  config.vm.define "ansiblecm" do |ansiblecm|
    ansiblecm.vbguest.auto_update = true
    ansiblecm.vm.hostname = "ansiblecm"
    ansiblecm.vm.network "private_network", ip: "192.168.56.231"
  end
end