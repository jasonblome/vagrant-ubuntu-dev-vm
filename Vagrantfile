# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'fileutils'

Vagrant.configure("2") do |config|
  # ubuntu 18.04 configuration
  config.vm.box = "hashicorp/bionic64"

  # setup X11 forwarding
  config.ssh.forward_agent = true
  config.ssh.forward_x11 = true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
  end

  FileUtils.mkdir_p './development'
  config.vm.synced_folder "./development", "/home/vagrant/development"
  config.vm.network "forwarded_port", guest: 8080, host: 8081

  config.vm.provision "shell", inline: <<-SHELL
    # add the apt repository for docker
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu/ $(lsb_release -cs) stable"

    # update the apt index
    apt update 

    # install the docker dependencies
    apt -y install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
    
    # install docker
    apt -y install docker-ce docker-ce-cli containerd.io

    # install utilities
    apt -y install emacs x11-apps xauth openjdk-8-jdk

    # install jetbrains IDEs
    snap install pycharm-professional --classic
    snap install intellij-idea-ultimate --classic
    snap install datagrip --classic

    # install VS Code
    snap install code --classic

    # install miniconda
    curl -o miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
    sh miniconda.sh -b -p /home/vagrant/install/anaconda/
    rm miniconda.sh

    # install apache directory studio for LDAP fun
    mkdir install
    curl -o apache-directory-studio.tgz http://mirror.cogentco.com/pub/apache/directory/studio/2.0.0.v20180908-M14/ApacheDirectoryStudio-2.0.0.v20180908-M14-linux.gtk.x86_64.tar.gz
    tar xvzf apache-directory-studio.tgz 
    mv ApacheDirectoryStudio/ install/
    rm apache-directory-studio.tgz 

    echo '/home/vagrant/install/anaconda/etc/profile.d/conda.sh' >> /home/vagrant/.bashrc 

    chown vagrant:vagrant -R install
  SHELL
end
