# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"

unless Vagrant.has_plugin?("vagrant-hostmanager")
  raise 'vagrant-hostmanager plugin is required'
end

provision = <<SCRIPT

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
