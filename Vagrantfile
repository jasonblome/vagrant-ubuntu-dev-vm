# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # ubuntu 18.04 configuration
  config.vm.box = "hashicorp/bionic64"

  # setup X11 forwarding
  config.ssh.forward_agent = true
  config.ssh.forward_x11 = true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
  end

  config.vm.synced_folder "./", "/vagrant"
  config.vm.network "forwarded_port", guest: 8080, host: 9080

  config.vm.provision "shell", inline: <<-SHELL
    # install ansible for the real provisioning steps
    apt-add-repository -y ppa:ansible/ansible
    apt update
    apt install -y ansible aptitude
    ansible-playbook -i /vagrant/ansible/inventory /vagrant/ansible/site.yml
  SHELL
end
