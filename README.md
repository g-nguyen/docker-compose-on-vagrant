# docker-compose-on-vagrant
Docker compose on Vagrant with sattic IP

## Installation
### Define your project's static IP with Vagrantfile
Vagrantfile
```
IP = "192.168.1.100"
```

### deploy your project's docker-compose.yml
```
vagrant-docker-compose
  |- Project_A/docker-comose.yml
  |- Project_B/docker-comose.yml
  |- ...
  |- Vagrantfile
```

### Launch
```
$ vagrant up --provision
```
or
```
$ vagrant up
$ vagrant provision
```
