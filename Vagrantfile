# -*- mode: ruby -*-
# vi: set ft=ruby :

# Set network info
HOST_IP = "192.168.33.10"
DNS = "10.0.2.3"
PUBLIC_NETWORK = "192.168.27"
VM_NAME = "devstack"
#
# # Set DevStack info
# DEVSTACK_BRANCH = "master"
# DEVSTACK_PASSWORD = "stack"

Vagrant.configure(2) do |config|
  config.vm.box = "Centos71"
  config.vm.define :devstack do |devstack|
      devstack.vm.hostname =  "#{VM_NAME}"
      devstack.vm.provider :libvirt do |domain|
      	domain.memory = 4096
      	domain.cpus = 2
      	domain.nested = true
      	domain.volume_cache = 'none'
      end
      #eth1,  API NETWORK will be the management endpoint
      devstack.vm.network :private_network, ip: "#{HOST_IP}", netmask: "255.255.255.0"
      #eth2, this will be the "public" VM network
      devstack.vm.network :private_network, ip: "#{PUBLIC_NETWORK}.2", netmask: "255.255.255.0", auto_config: false 
     
      # yum update
      config.vm.provision "shell", inline: <<-EOF
      yum update -y
      yum install -y git
      EOF
  end
end
