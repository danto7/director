# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/stretch64"
  config.vm.define "test_server"

  config.vm.provision "ansible" do |a|
    a.groups = {"kube_nodes": ["test_server"]}
    a.playbook = "server.yml"
  end
end
