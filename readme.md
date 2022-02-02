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

### Automating the dependencies By Using provision.sh
- add `sudo apt-get install nodejs -y`
- add `sudo apt-get install python-software-properties`
- add `curl -sl https://deb.nodesource.com/setup_6.x | sudo -E bash -`
- add `sudo apt-get install nodejs -y`
- add `sudo npm install pm2 -g`
#### This will allow the dependecies to install as soon as you run the machine and all I had to do after this was go on the app directory on the virtual machine and type `npm install` then `npm start`.

## Linux Variables
- vreate Linux variables `FIRST_NAME=ARMAAN`
- How to check the variable `echo $FIRST_NAME`

## Environment Variables
- How to check `env var`
- command `printenv "key"` or `env`
- create environment variable `export`
- `export LAST_NAME=ALAM` 
- how to make environment variable persistent `vim ~/.bashrc` then add the variable into this file and save it then type `source ~/.bashrc`
- how to delete a enviroment variable `unset LAST_NAME`
- how to kill a process
- how to use grep & | 

## Nginx Reverse Proxy
- `sudo nano /etc/nginx/sites-available/default`
- in this file find "location/" and add:
```
location / {
                proxy_pass http://localhost:3000;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
    }
```
- `sudo nginx -t`
- `sudo systemctl restart nginx`
- go into app and start the app

## Creating two VMs
- go back into vagrantfile and change to:
```

Vagrant.configure("2") do |config|
    config.vm.define "app" do |app|
        # creating a virtual machine ubuntu 
        config.vm.box = "ubuntu/xenial64"

        # creating a private network with ip
        config.vm.network "private_network", ip: "192.168.10.100"

        # creating a synced_folder
        config.vm.synced_folder ".", "/home/vagrant/app"

        # Provisioning
        config.vm.provision "shell", path: "provision.sh"
        end
    config.vm.define "db" do |db|
        config.vm.box = "ubuntu/xenial64"
        db.vm.network "private_network", ip: "192.168.10.150"
        end
end
```
#### you can create more vms by adding more config.vm.define's

- `vagrant up`
- to enter a vm type `vagrant ssh "VM-NAME"

- sudo nano /etc/nginx/sites-available/default
- sudo nginx -t
- sudo systemctl restart nginx

### Blocker
- while trying to run the application again because I edited files to try to get nginx to work I altered files I shouldn't have to fix this I went to virtual-box and removed the virtual machines and done vagrant up again and everything worked out. After a while my reverse proxy wasnt working working so i done a vagrant reload and it started working again.
