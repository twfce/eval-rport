# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  
  config.vm.define "rport-server" do |rport|
    rport.vm.box = "ubuntu/jammy64"
    rport.vm.hostname = "rport-server"
    rport.vm.network "private_network", ip: "192.168.56.10"
    rport.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
    end

   config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get upgrade -y
    curl -o rportd-installer.sh https://get.rport.io
    bash rportd-installer.sh \
      --email admin@example.com \
      --fqdn rport.local \
      --no2fa \
      --skip-nat
    echo -e "127.0.0.1 localhost\n127.0.1.1 rport-server\n127.0.0.1 rport.local" | tee /etc/hosts
   SHELL
  end
  
  config.vm.define "rport-server" do |rport|
    rport.vm.box = "ubuntu/jammy64"
    rport.vm.hostname = "rport-client"
    rport.vm.network "private_network", ip: "192.168.56.11"
    rport.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
    end

   config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get upgrade -y
    echo -e "127.0.0.1 localhost\n127.0.1.1 rport-server\n127.0.0.1 rport.local"
   SHELL
  end  
end
