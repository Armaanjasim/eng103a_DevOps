# What is DevOps
## Why DevOps
### Benefits of DevOps

** Four pillars of DevOps best practice**
- Ease of Us
- Flexibility
- Robustness - faster delivery of product
- Cost - cost effective

### Monolith, 2 tier & MicroServices Architectures

&nbsp;

# Virutal Machine
## Install Ruby
- https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.6.6-1/rubyinstaller-devkit-2.6.6-1-x64.exe
- Check version by "ruby --version"
## Install Vagrant 
- https://www.vagrantup.com/
- Check version by "vagrant --version"
## Install Virtual Box
- https://www.virtualbox.org/wiki/Downloads
- After installation go to Control Panel > Network and Internet > Network and Sharing Centre > Change Adapter Settings. 
- In this right click VirtualBox Host-Only Network and choose Properties.
- Click Install > Service > Manufacturer > Oracle Corporation > Network Service > VirtualBox NDIS6 Bridged Networking Driver
- Then finally add a vagrantfile where you want to setup the virtual machine and add: 
 
&nbsp;
```
Vagrant.configure("2") do |config|

 config.vm.box = "ubuntu/xenial64"

end
```
&nbsp;

## VM Commands
- create a VM `vagrant up`
- check status `vagrant status`
- delete a VM `vagrant destroy`
- pause a VM `vagrant halt`
- update a VM `vagrant reload`
- access a VM `vagrant ssh`

## Linux Commands
- act as an admin `sudo`
- update VM `sudo apt-get update`
- upgrade VM `sudo apt-get upgrade`
- install VM `sudo apt-get install`
- remove VM `sudo apt-get remove`
- systemctl `status/restart/start/stop nginx`
- installing nginx `sudo apt-get install nginx`

## Starting VM Guide
- `vagrant up` in the terminal in the directory where vagrant is downloaded
- edit the vargrantfile and add:
  ```
  config.vm.network "private_network", ip: "192.168.10.100"
  ```
- once this is done enter the virtual machine by typing `vagrant ssh`
- type `sudo apt-get update` and then after `sudo apt-get upgrade -y`
- then finally type `sudo apt-get install nginx` you can then see if it is installed by using `systemctl status nginx`
- you can then go to the browser and type 192.168.10.100 if there is a connection