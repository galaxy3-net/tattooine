# -*- mode: ruby -*-
# vi: set ft=ruby :

#  https://github.com/rapid7/metasploitable3

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

    ub1404.vm.network "private_network", ip: '10.55.56.50',
    	virtualbox__intnet: "metasploitable3",
    	nic_type: "virtio"

    ub1404.vm.provider "virtualbox" do |v|
      v.name = "Tatttoine (Metasploitable3-ub1404)"
      v.memory = 2048

      #v.customize ['modifyvm', :id, '--nic0', 'intnet']
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

  config.vm.define "win2k8" do |win2k8|
    # Base configuration for the VM and provisioner
    win2k8.vm.box = "rapid7/metasploitable3-win2k8"
    win2k8.vm.hostname = "metasploitable3-win2k8"
    win2k8.vm.communicator = "winrm"
    win2k8.winrm.retry_limit = 60
    win2k8.winrm.retry_delay = 10

	win2k8.vbguest.auto_update = false

    #win2k8.vm.network "private_network", type: "dhcp"
    #ub1404.vm.network "private_network", ip: '10.55.55.50'
	win2k8.vm.network "private_network", ip: '10.55.56.51',
		virtualbox__intnet: "metasploitable3"

    win2k8.vm.provider "virtualbox" do |v|
      v.name = "Tatttoine (metasploitable3-win2k8)"
      v.memory = 4096
      v.cpus = 2
      v.video_type = 'qxl'
      v.input :type => "tablet", :bus => "usb"
      v.channel :type => 'unix', :target_name => 'org.qemu.guest_agent.0', :target_type => 'virtio'
      v.channel :type => 'spicevmc', :target_name => 'com.redhat.spice.0', :target_type => 'virtio'
      v.graphics_type = "spice"

      v.customize ['modifyvm', :id, '--nictype0', 'virtio']
      v.customize ['modifyvm', :id, '--nicpromisc0', 'allow-all']
      v.customize ['modifyvm', :id, '--nictype1', 'virtio']
      v.customize ['modifyvm', :id, '--nicpromisc1', 'allow-all']
      v.customize ['modifyvm', :id, '--nictype2', 'virtio']
      v.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all']
      v.customize ['modifyvm', :id, '--nictype3', 'virtio']
      v.customize ['modifyvm', :id, '--nicpromisc3', 'allow-all']

    end

    win2k8.vm.provider "libvirt" do |v|
      v.name = "Tatttoine (metasploitable3-win2k8)"
      v.memory = 4096
      v.cpus = 2
      v.video_type = 'qxl'
      v.input :type => "tablet", :bus => "usb"
      v.channel :type => 'unix', :target_name => 'org.qemu.guest_agent.0', :target_type => 'virtio'
      v.channel :type => 'spicevmc', :target_name => 'com.redhat.spice.0', :target_type => 'virtio'
      v.graphics_type = "spice"

      #v.customize ['modifyvm', :id, '--nic0', 'intnet']
      v.customize ['modifyvm', :id, '--nictype0', 'virtio']
      v.customize ['modifyvm', :id, '--nicpromisc0', 'allow-all']
      v.customize ['modifyvm', :id, '--nictype1', 'virtio']
      v.customize ['modifyvm', :id, '--nicpromisc1', 'allow-all']
      v.customize ['modifyvm', :id, '--nictype2', 'virtio']
      v.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all']
      v.customize ['modifyvm', :id, '--nictype3', 'virtio']
      v.customize ['modifyvm', :id, '--nicpromisc3', 'allow-all']

      # Enable Hyper-V enlightenments: https://blog.wikichoon.com/2014/07/enabling-hyper-v-enlightenments-with-kvm.html
      v.hyperv_feature :name => 'stimer',  :state => 'on'
      v.hyperv_feature :name => 'relaxed', :state => 'on'
      v.hyperv_feature :name => 'vapic',   :state => 'on'
      v.hyperv_feature :name => 'synic',   :state => 'on'
    end

    # Configure Firewall to open up vulnerable services
    case ENV['MS3_DIFFICULTY']
      when 'easy'
        win2k8.vm.provision :shell, inline: "C:\\startup\\disable_firewall.bat"
      else
        win2k8.vm.provision :shell, inline: "C:\\startup\\enable_firewall.bat"
        win2k8.vm.provision :shell, inline: "C:\\startup\\configure_firewall.bat"
    end

    # Insecure share from the Linux machine
    win2k8.vm.provision :shell, inline: "C:\\startup\\install_share_autorun.bat"
    win2k8.vm.provision :shell, inline: "C:\\startup\\setup_linux_share.bat"
    #win2k8.vm.provision :shell, inline: "rm C:\\startup\\*" # Cleanup startup scripts
  end

end
