# -*- mode: ruby -*-
# vi: set ft=ruby :

# README
#
# Getting Started:
# 1. vagrant plugin install vagrant-hostmanager
# 2. vagrant up
# 3. vagrant ssh
#
# This should put you at the control host
#  with access, by name, to other vms

# Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

Vagrant.configure(2) do |config|
  config.hostmanager.enabled = true
# Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = false

  config.vm.box = "ubuntu/trusty64"

  config.vm.define "control", primary: true do |h|
    h.vm.network "private_network", ip: "192.168.135.10"
    h.vm.hostname = "control"
    h.vm.provision :shell, :inline => <<'EOF'
if [ ! -f "/home/vagrant/.ssh/id_rsa" ]; then
  ssh-keygen -t rsa -N "" -f /home/vagrant/.ssh/id_rsa
fi
cp /home/vagrant/.ssh/id_rsa.pub /vagrant/control.pub

cat << 'SSHEOF' > /home/vagrant/.ssh/config
Host *
  StrictHostKeyChecking no
  UserKnownHostsFile=/dev/null
SSHEOF

chown -R vagrant:vagrant /home/vagrant/.ssh/
EOF
  end

############################################################
#
config.vm.provider "virtualbox" do |control|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     control.memory = "1024"
     control.name = "Ansible-control"
  #   vb.name = "git-box"
  end
###########################################################


  config.vm.define "lb01" do |h|
    h.vm.network "private_network", ip: "192.168.135.101"
    h.vm.hostname = "lb01"
    h.vm.provision :shell, inline: 'cat /vagrant/control.pub >> /home/vagrant/.ssh/authorized_keys'
  end

###########################################################
#
config.vm.provider "virtualbox" do |lb01|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     lb01.memory = "1024"
     lb01.name = "Ansible-lb01"
  #   vb.name = "git-box"
  end

############################################################

  config.vm.define "app01" do |h|
    h.vm.network "private_network", ip: "192.168.135.111"
    h.vm.hostname = "app01"
    h.vm.provision :shell, inline: 'cat /vagrant/control.pub >> /home/vagrant/.ssh/authorized_keys'
  end
#############################################################
#
config.vm.provider "virtualbox" do |app01|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     app01.memory = "1024"
     app01.name = "Ansible-app01"
  #   vb.name = "git-box"
  end

#############################################################

  config.vm.define "app02" do |h|
    h.vm.network "private_network", ip: "192.168.135.112"
    h.vm.hostname = "app02"
    h.vm.provision :shell, inline: 'cat /vagrant/control.pub >> /home/vagrant/.ssh/authorized_keys'
  end
#############################################################
#
config.vm.provider "virtualbox" do |app02|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     app02.memory = "1024"
     app02.name = "Ansible-app02"
  #   vb.name = "git-box"
  end



  config.vm.define "db01" do |h|
    h.vm.network "private_network", ip: "192.168.135.121"
    h.vm.hostname = "db01"
    h.vm.provision :shell, inline: 'cat /vagrant/control.pub >> /home/vagrant/.ssh/authorized_keys'
  end
###############################################################
#
config.vm.provider "virtualbox" do |db|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     db.memory = "1024"
     db.name = "Ansible-db01"
  #   vb.name = "git-box"
  end
##############################################################
end
