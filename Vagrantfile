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
      a.extra_vars = {additional_sans: "192.168.77.21", advertise_address: "192.168.77.21"}
    end
  end

  config.vm.define "node" do |node|
    node.vm.hostname = "node"
    node.vm.network "private_network", ip: "192.168.77.22"

    node.vm.provision "ansible" do |a|
      a.limit = "all"
      a.groups = {"kube_node": ["node"]}
      a.playbook = "kube_node.yml"
      a.extra_vars = {master_host: "192.168.77.21:6443"}
    end
  end
end
