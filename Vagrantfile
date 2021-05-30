# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.define "ubuntu" do |ubuntu|
    config.vm.box = "ubuntu/focal64"

    config.vm.network "forwarded_port", guest: 2375, host: 12375

    config.vm.provider "virtualbox" do |vb|
      vb.memory = "2056"
      vb.cpus = 2
    end

    config.vm.provision "docker"
    config.vm.provision "file", source: "./override.conf", destination: "/tmp/override.conf"
    config.vm.provision "shell", inline: <<-SHELL
      # allow to connect docker server port
      sudo iptables -A INPUT -p tcp --dport 2375   -j ACCEPT
      sudo iptables -A INPUT -p tcp --dport 2376   -j ACCEPT
      # put conf file
      sudo mkdir -p /etc/systemd/system/docker.service.d/
      sudo cp /tmp/override.conf /etc/systemd/system/docker.service.d/override.conf
      # Reload the systemctl configuration
      sudo systemctl daemon-reload
      # Restart Docker
      sudo systemctl restart docker.service
    SHELL
  end
end
