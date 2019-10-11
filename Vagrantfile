# -*- mode: ruby -*-
# vi: set ft=ruby :


#BOX_BASE = "centos/7"
# for centos 8 
BOX_BASE = "generic/centos8"

$nodejssetup = <<-SCRIPT
sudo yum install epel-release -y
sudo dnf config-manager --set-enabled PowerTools
sudo dnf install nodejs -y
sudo systemctl stop firewalld
sudo echo "LANG=en_US.utf-8" > /etc/environment
sudo echo "LC_ALL=en_US.utf-8" >> /etc/environment
SCRIPT


Vagrant.configure("2") do |config|

    config.vm.define "nodejs" do |nodejs|

         # Box
         nodejs.vm.box = BOX_BASE

         nodejs.vm.network "forwarded_port", guest: 8000, host: 8000
         nodejs.vm.network "forwarded_port", guest: 8080, host: 8080
         # Memory and CPU allocation
         nodejs.vm.provider "virtualbox" do |v|
            v.memory = 512
            v.cpus = 1
         end

         # IP allocation
         # nodejs.vm.network "private_network", ip: "192.168.22.10", virtualbox__intnet: "mynetwork01"

         # Host name allocation
         nodejs.vm.hostname = "nodejs.example.com"
         
        
         nodejs.vm.synced_folder ".", "/vagrant", type: "virtualbox"

         # Installing required packages for ansible controller node
         nodejs.vm.provision "shell", inline: $nodejssetup
     end

end
