# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"

unless Vagrant.has_plugin?("vagrant-hostmanager")
  raise 'vagrant-hostmanager plugin is required'
end

provision = <<SCRIPT
export http_proxy=http://proxy.lbs.alcatel-lucent.com:8000
export https_proxy=https://proxy.lbs.alcatel-lucent.com:8000
echo "http_proxy=$http_proxy" >> /etc/environment
echo "https_proxy=$https_proxy" >> /etc/environment

curl http://files.fast.ai/setup/paperspace | bash

SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.provider "libvirt" do |libvirt, override|
    libvirt.cpus = 8 
    libvirt.memory = 16384 
    libvirt.driver = 'kvm'
    libvirt.machine_virtual_size = 100
    override.vm.box = "nrclark/xenial64-minimal-libvirt"
  end

  config.vm.define "fastai" do |fastai|
    fastai.vm.provision "shell", inline: provision
  end
end
