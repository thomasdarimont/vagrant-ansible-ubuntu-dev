# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.box = "bento/ubuntu-16.04"
  
  config.ssh.username = "vagrant"
  config.ssh.password = "vagrant"
  config.ssh.forward_agent = true
  
  config.vm.network :private_network, ip: "192.168.33.39"
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |v|
    
    v.name = "ubuntu.dev"
    v.memory = 8192
    v.cpus = 4

# Set Video Memory to 32mb
    v.customize [
        "modifyvm", :id, 
        "--vram", "32"
    ]

# Connect the "network cable" on the nat interface
    v.customize [
        "modifyvm", :id,
        "--cableconnected1", "on",
    ]

# https://serverfault.com/questions/453185/vagrant-virtualbox-dns-10-0-2-3-not-working
    v.customize [
        "modifyvm", :id, 
        "--natdnsproxy1", "on"
    ]
    v.customize [
        "modifyvm", :id, 
        "--natdnshostresolver1", "on"
    ]
  end

  # Enable provisioning with Ansible.
  config.vm.provision :ansible do |ansible|
    ansible.extra_vars = { 
#        remote_user: "vagrant"
    }
    ansible.playbook = "./provisioning/playbook.yml"
    ansible.inventory_path = "./provisioning/inventory"
    ansible.limit = "all"
    ansible.verbose = "vvv"
  end
end