# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/stretch64"

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end

  config.vm.define "master", primary: true do |master|
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "192.168.77.21"

    master.vm.provision "ansible" do |a|
      a.groups = {"kube_master": ["master"]}
      a.playbook = "kube_master.yml"
    end
  end

  config.vm.define "node" do |node|
    node.vm.hostname = "node"
    node.vm.network "private_network", ip: "192.168.77.22"

    node.vm.provision "ansible" do |a|
      a.limit = "all"
      a.groups = {"kube_node": ["node"]}
      a.playbook = "kube_node.yml"
    end
  end
end
