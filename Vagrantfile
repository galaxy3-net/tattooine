# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.synced_folder '.', '/vagrant', disabled: true

  config.vm.define "ub1404" do |ub1404|
    ub1404.vm.box = "rapid7/metasploitable3-ub1404"
    ub1404.vm.box_version = "0.1.12-weekly"
    ub1404.vm.hostname = "tattoine"
    ub1404.ssh.username = 'vagrant'
    ub1404.ssh.password = 'vagrant'

    ub1404.vbguest.auto_update = false
    ub1404.ssh.insert_key = false
    ub1404.ssh.connect_timeout = 20
    ub1404.vm.boot_timeout = 120

    ub1404.vm.network "private_network", ip: '10.55.55.50'

    ub1404.vm.provider "virtualbox" do |v|
      v.name = "Tatttoine (Metasploitable3-ub1404)"
      v.memory = 2048
      v.customize ['modifyvm', :id, '--nictype0', 'virtio']
      v.customize ['modifyvm', :id, '--nicpromisc0', 'allow-all']
      v.customize ['modifyvm', :id, '--nictype1', 'virtio']
      v.customize ['modifyvm', :id, '--nicpromisc1', 'allow-all']
      v.customize ['modifyvm', :id, '--nictype2', 'virtio']
      v.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all']
      v.customize ['modifyvm', :id, '--nictype3', 'virtio']
      v.customize ['modifyvm', :id, '--nicpromisc3', 'allow-all']
    end
  end
end
