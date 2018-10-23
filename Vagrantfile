# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  #-------------------------------------------------------------------------------
  # all server
  #-------------------------------------------------------------------------------
  config.vm.box = "centos/7"
  config.ssh.insert_key = false
  config.vm.provision "file", source: "/mnt/c/Users/hoge/.vagrant.d/insecure_private_key", destination: "~/.ssh/id_rsa"
  config.vm.provision "shell", inline: "sudo chmod 600 /home/vagrant/.ssh/id_rsa"
  config.vm.provision "shell", path: "./vagrant/provision_proxy.sh"

  #-------------------------------------------------------------------------------
  # ansible server
  #-------------------------------------------------------------------------------
  config.vm.define "ansible" do |as|
    as.vm.provider "virtualbox" do |vb|
      vb.gui = true  
      vb.memory = "512"
    end
    as.vm.hostname = "ansible"
    as.vm.network "private_network", ip: "192.168.33.10"
    as.vm.provision "shell", path: "./vagrant/provision_ansible.sh"
  end

  #-------------------------------------------------------------------------------
  # node server
  #-------------------------------------------------------------------------------
  (1..2).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.provider "virtualbox" do |vb|
        vb.gui = true
        vb.memory = "512"
      end
      node.vm.hostname = "node#{i}"
      node.vm.network "private_network", ip: "192.168.33.3#{i}"
    end
  end

end
