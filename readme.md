# What is DevOps
## Why DevOps
### Benefits of DevOps

**Four pillars of DevOps best practice**
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
&nbsp;
  ```
  config.vm.network "private_network", ip: "192.168.10.100"
  ```
- once this is done enter the virtual machine by typing `vagrant ssh`
- type `sudo apt-get update` and then after `sudo apt-get upgrade -y`
- then finally type `sudo apt-get install nginx` you can then see if it is installed by using `systemctl status nginx`
- you can then go to the browser and type 192.168.10.100 if there is a connection

## Linux Basics

### Commands

- who am I `uname -a`
- where am I `pwd`
- list directory/files `ls`
- list hidden folders aswell `ls -a`
- make a directory `mkdir "name of directory"`
- navigate to directory `cd "name of directory"`
- how to create a file `touch "file-name"` or `vim "file-name"`
- display content of the file `cat "file-name"`
- how to remove file `rm -rf "file-name"`
- how to copy a file `cp "file-destination-name" final desination`
- how to move a file `mv "file-name" final destination`
- how to check running processes `top`

### Permissions
- READ Write Executable read only
- how to check permissions `ll`
- change permission `chmod permission "file-name"`

### Bash scripting
- let the system know its a bash script `#!/bin/bash` at the top of the document

### Provision.sh
- add `#!/bin/bash`
- add `sudo apt-get update`
- add `sudo apt-get upgrade`
- add `sudo apt-get install nginx -y`

## Checking Dependencies & Runnning App  
- on local host:
  - `gem install bundler`
  - `bundle`
  - `rake spec`
    - this gave me 3 failures which i had to install on the vm. No nodejs, v6 required and npm install on the vm.
- on virtual machine:
  - started by using `sudo apt-get install nodejs -y` however the correct version didnt download.
  - then used `sudo apt-get install python-software-properties` 
  - to install v6 i used this command with the link:
```

curl -sl https://deb.nodesource.com/setup_6.x | sudo -E bash -

```
- carrying on in virtual machine:
  - i then used `sudo apt-get install nodejs -y` to actually install the correct version
  - finally i done `sudo npm install pm2 -g`
- on local host:
  - used `rake spec` which gave me 0 failures
- on virtual machine:
  - went to the `app` directory where i wanted to run the application and followed the instructions on the readme file which was `npm install` then `npm start` and it gave me the correct message "app is ready and listening on port 3000"