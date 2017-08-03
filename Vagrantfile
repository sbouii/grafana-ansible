# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  
   config.vm.box = "debian/jessie64"
  
   config.vm.box_check_update = false

   # Disable the default /vagrant share
   config.vm.synced_folder "../data", "/vagrant_data" , disabled: true

   config.vm.define "ansible_vm" do |cfg|
    cfg.vm.network "private_network", ip: "192.168.33.101"
    cfg.vm.hostname = "ansible_vm"    
    cfg.vm.provider "virtualbox" do |vb|
     vb.gui = true
     vb.name = 'ansible_vm'
     vb.memory = "1750"
    end
    cfg.vm.provision :ansible do |ansible|
     ansible.playbook = 'provision.yml'
     ansible.inventory_path = 'vagrant-inventory.ini'
     ansible.limit = 'ansible_vm'
     ansible.verbose = 'v'
    end
   end
end
