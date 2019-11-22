# -*- mode: ruby -*-
# vi: set ft=ruby :

## define IP for your project
IP = "192.168.1.4"

Vagrant.configure("2") do |config|
  config.vm.box = "AlbanMontaigu/boot2docker"

  # network
  config.vm.network "public_network",
  	ip: IP,
	netmask: "255.255.0.0",
	bridge: "bond0"

  # shared folder
  config.vm.synced_folder "./", "/vagrant"

  # install docker-compose
  config.vm.provision "shell",
  name: "install docker-compose",
  inline: <<-SHELL
    if ! which docker-compose; then
      sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
      chmod +x /usr/local/bin/docker-compose
    fi
  SHELL

  # run docker by docker-compose
  config.vm.provision "shell",
  name: "run docker-compose",
  inline: <<-SHELL
    find /vagrant -name docker-compose.yml |xargs -n1 -i /usr/local/bin/docker-compose -f {} up -d
  SHELL
end
