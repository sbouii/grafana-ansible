# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  
   config.vm.box = "geerlingguy/centos7"
   config.ssh.insert_key = false  
   config.vm.box_check_update = false

   # Disable the default /vagrant share
   config.vm.synced_folder "../data", "/vagrant_data" , disabled: true
  
   config.vm.define "ansible-vm" do |cfg|
    cfg.vm.network "private_network", ip: "192.168.33.11"
    cfg.vm.hostname = "ansible-vm"        
    cfg.vm.provider "virtualbox" do |vb|
     vb.gui = true
     vb.name = 'ansible-vm'
     vb.memory = "1200"
    end
    cfg.vm.provision :ansible do |ansible|
     ansible.playbook = 'provision.yml'
     ansible.inventory_path = 'vagrant-inventory.ini'
     ansible.limit = 'ansible-vm'
     ansible.verbose = 'v'
    end
   end
end
