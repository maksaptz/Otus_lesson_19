# -*- mode: ruby -*-:
# vi: set ft=ruby :

#разрешаем увеличивать диски
# export VAGRANT_EXPERIMENTAL="disks"

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.box_version = "2004.01"

  config.vm.define "pxeserver" do |server|
    server.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end    
    server.vm.disk :disk, size: "15GB", name: "extra_storage1"
    server.vm.host_name = 'pxeserver'
    server.vm.network "private_network", 
                       ip: "192.168.50.10",
		       adapter: 2,
                       virtualbox__intnet: "pxenet" 
    server.vm.network "private_network",
                       ip: "192.168.40.10",
                       adapter: 3

    server.vm.network "forwarded_port", guest: 80, host: 8081
 
    server.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/play.yml"
      ansible.inventory_path = "ansible/hosts"
      ansible.host_key_checking = "false"
      ansible.limit = "all"
    end
  end
  
  config.vm.define "pxeclient" do |pxeclient|
    pxeclient.vm.host_name = 'pxeclient'
    pxeclient.vm.network "private_network", 
                          ip: "192.168.50.11",
                          virtualbox__intnet: "pxenet"
    pxeclient.vm.provider :virtualbox do |vb|
      vb.memory = "2048"
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize [
          'modifyvm', :id,
          '--nic1', 'intnet',
          '--intnet1', 'pxenet',
          '--nic2', 'nat',
          '--boot1', 'net',
          '--boot2', 'none',
          '--boot3', 'none',
          '--boot4', 'none'
        ]
      end
  
  end
  
end
