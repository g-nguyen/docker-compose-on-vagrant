# -*- mode: ruby -*-
# vi: set ft=ruby :

## define IP for your project
IP = "192.168.1.100"

Vagrant.configure("2") do |config|
  config.vm.box = "ailispaw/barge"

  # network
  config.vm.network "public_network",
  	ip: IP,
	netmask: "255.255.0.0",
	bridge: "bond0"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
    vb.customize [
      "modifyvm", :id,
      "--nicpromisc2","allow-all",
      "--vram", "256",
    ]
  end

  # shared folder
  config.vm.synced_folder "./", "/vagrant"

  # update docker
  config.vm.provision "shell",
  name: "update docker",
  inline: <<-SHELL
    sudo /etc/init.d/docker restart 18.06.1-ce
  SHELL

  # install docker-compose
  config.vm.provision "shell",
  name: "install docker-compose",
  inline: <<-SHELL
    if ! which docker-compose; then
      sudo wget "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -O /usr/bin/docker-compose
      sudo chmod +x /usr/bin/docker-compose
    fi
  SHELL

  # run docker by docker-compose
  config.vm.provision "shell",
  name: "run docker-compose",
  inline: <<-SHELL
    find /vagrant -name docker-compose.yml |xargs -n1 -i /usr/bin/docker-compose -f {} up -d
  SHELL
end
