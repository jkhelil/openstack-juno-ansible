# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "trusty64"
 
  
  config.vm.define "controller" do |machine|
    machine.vm.network :private_network, ip: "10.11.0.2", :netmask => "255.255.255.0"
    machine.vm.network :private_network, ip: "10.12.0.2", :netmask => "255.255.255.0"
    machine.vm.network :private_network, ip: "10.14.0.2", :netmask => "255.255.255.0"
    machine.vm.network :private_network, ip: "10.15.0.2", :netmask => "255.255.255.0"
    machine.vm.network :private_network, ip: "10.16.80.2", :netmask => "255.255.255.0"
    machine.vm.hostname = "controller"
    machine.vm.provider :virtualbox do |v| 
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

  config.vm.define "compute" do |machine|
    machine.vm.network :private_network, ip: "10.11.0.3", :netmask => "255.255.255.0"
    machine.vm.network :private_network, ip: "10.13.0.3", :netmask => "255.255.255.0"
    machine.vm.hostname = "compute"
    machine.vm.provider :virtualbox do |v| 
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

  config.vm.define "network" do |machine|
    machine.vm.network :private_network, ip: "10.11.0.4", :netmask => "255.255.255.0"
    machine.vm.network :private_network, ip: "10.13.0.4", :netmask => "255.255.255.0"
    machine.vm.network :private_network, ip: "10.14.0.4", :netmask => "255.255.255.0"
    machine.vm.hostname = "network"
    machine.vm.provider :virtualbox do |v| 
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--nicpromisc4", "allow-all"]
    end
  end

  config.vm.define "image" do |machine|
    machine.vm.network :private_network, ip: "10.11.0.5", :netmask => "255.255.255.0"
    machine.vm.hostname = "image"
    machine.vm.provider :virtualbox do |v| 
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

  cinder_file_to_disk = '.vagrant/cinder-volume-extradisk.vdi'
  config.vm.define "volume" do |machine|
    machine.vm.network :private_network, ip: "10.11.0.6", :netmask => "255.255.255.0"
    machine.vm.hostname = "volume"
    machine.vm.provider :virtualbox do |v| 
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["createhd", "--filename", cinder_file_to_disk, "--size", 4096]
      v.customize ["storageattach", :id, "--storagectl", "SATAController",
                   "--port", 2, "--device", 0, "--type", "hdd",
                   "--medium", cinder_file_to_disk]
    end
  end

end
