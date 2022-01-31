# What is DevOps
## Why DevOps
### Benefits of DevOps

** Four pillars of DevOps best practice**
- Ease of Us
- Flexibility
- Robustness - faster delivery of product
- Cost - cost effective

### Monolith, 2 tier & MicroServices Architectures
#
#
#
#
# Virutal Machine Installation
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

Vagrant.configure("2") do |config|

 config.vm.box = "ubuntu/xenial64"

end


- create a VM `vagrant up`
- check status `vagrant status`
- delete a VM `vagrant destroy`
- pause a VM `vagrant halt`
- update a VM `vagrant reload`
- access a VM `vagrant ssh`