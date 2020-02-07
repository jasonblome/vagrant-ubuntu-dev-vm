# Ubuntu Development VM

This repository contains a Vagrantfile and ansible playbook to build my development environment. This VM is based on the Hashicorp Ubuntu 18.04 LTS release (Bionic Beaver) and will install the following software:

* Development Tools
  * gcc/g++ standard libraries and manpages
  * Miniconda for python development
  * OpenJDK 8
  * Intellij Ultimate
  * Pycharm Professional
  * Datagrip
* Editors
  * Emacs
  * SublimeText
  * VS Code
* System Tools
  *  X11
  * telnet, ftp, dnsutils, net-tools, wget, whois

## Requirements

Software packages for VirtualBox, Vagrant, and XQuartz need to be installed prior to building this VM.

## Running

Simply run 'vagrant up' from the root directory of this repository to build the machine.