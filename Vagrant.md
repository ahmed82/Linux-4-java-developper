# Vagrant
## Vagrant: 
is a tool for building and managing virtual machine environments in a single workflow. 
a.	CLI tool for managing virtual machines.
b.	Workflow automated by way of Vagrant file. 
```
$> vagrant up 		Starts the VM
$> vagrant ssh 		Log into the VM
$> vagrant halt 		Gracefully shuts down the VM
$> vagrant destroy 	Deletes the VM
```
•	Update the Vagrantfile
Config.vm.box = “acloudfan/hlfdev2.0-0”

```
vagrant box list
vagrant status
vagrant destroy -f
```

## Create Vagrent 
This command create a singl file that hold the Vagrant configuration with the name `Vagrantfile`
```
vagrant init
```

## /vagrant 
The /vagrant directory in the VM it is mount to the host directory contain the vagrentfile.
So you can use subfile in the host machine and use them in the VM machine (if you want to share Script or Software with the VM).
Destroy the VM Not effecting the `/vagrant/script/`.
