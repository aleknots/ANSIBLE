# -*- mode: ruby -*-
# vi: set ft=ruby  :

# Antes de iniciar o vagrant up, é necessário instalar os plugins abaixo.

# vagrant plugin install vagrant-vbguest
# vagrant plugin install vagrant-group
# vagrant plugin install virtualbox

 ### RED HAT CENTOS

Vagrant.configure("2") do |config|

  config.vbguest.auto_update = false
  config.vm.box_check_update = false
  config.vm.define "srv-vm-jks01" do |conf|
  conf.vm.provision "shell", inline: <<-SHELL
    sudo sed -in 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
    sudo service sshd restart
 SHELL
    conf.vm.box = "centos/7"
    conf.vm.hostname = 'srv-vm-jks01.ansible'
    conf.vm.network "private_network", ip: "10.10.10.20"
    conf.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.name = "srv-vm-jks01"
      vb.memory = 2048
      vb.cpus = 2
      vb.customize ["modifyvm", :id, "--groups", "/CLOUD ANSIBLE"]

    end
  end

 ### CANONICAL UBUNTU

  config.vbguest.auto_update = false
  config.vm.box_check_update = false
  config.vm.provision "shell", inline: <<-SHELL
  sudo sed -in 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
  sudo service sshd restart
SHELL
  config.vm.define "srv-vm-dkr01" do |conf|
    conf.vm.box = "ubuntu/focal64"
    conf.vm.hostname = 'srv-vm-dkr01.ansible'
    conf.vm.network "private_network", ip: "10.10.10.21"
    conf.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.name = "srv-vm-dkr01"
      vb.memory = 2048
      vb.cpus = 2
      vb.customize ["modifyvm", :id, "--groups", "/CLOUD ANSIBLE"]

    end
  end

  config.group.groups = {
  "jenkins" => [
    "srv-vm-jks01",
  ],
  "docker" => [
    "srv-vm-dkr01",
  ],

 }

end