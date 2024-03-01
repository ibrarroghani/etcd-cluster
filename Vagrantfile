# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "bootstrap.sh"

  # etcd cluster nodes
  NodeCount = 3

  (1..NodeCount).each do |i|

    config.vm.define "etcd#{i}" do |etcdnode|

      etcdnode.vm.box               = "generic/ubuntu2004"
      etcdnode.vm.box_check_update  = false
      etcdnode.vm.box_version       = "3.3.0"
      etcdnode.vm.hostname          = "etcd#{i}.example.com"

      etcdnode.vm.network "private_network", ip: "192.168.56.1#{i}"
      
      etcdnode.vm.provider :virtualbox do |v|
        v.name    = "etcd#{i}"
        v.memory  = 1024
        v.cpus    = 1
      end
      
      etcdnode.vm.provider :libvirt do |v|
        v.memory  = 1024
        v.nested  = true
        v.cpus    = 1
      end
    
    end

  end

end
