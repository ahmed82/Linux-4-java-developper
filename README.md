# Linux
Repository contain all kubernetes and Linux note 

## usfull commands:
Disable Sudo Password Prompt Per Session
```
sudo -i
```
Disable Permanently
```
sudo visudo
```
At the bottom of the file, paste in the following, replacing username with your own.
```
username ALL=(ALL) NOPASSWD:ALL
```
Extend Inactivity Timeout
```
Defaults env_reset,timestamp_timeout=60
```
## download RPM package
```
sudo yum install wget
wget https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.2-3.el7.x86_64.rpm
```
The system should reach out to the website and download the file to your current working directory.
## Install Package
```
1- sudo rpm –i containerd.io-1.2.2-3.el7.x86_64.rpm
or
2- sudo yum localinstall containerd.io-1.2.2-3.el7.x86_64.rpm
```
## Find installed Package
```
rpm -qa | grep containerd.io
```
## Remove a RPM Package
```
sudo rpm -e containerd.io-1.2.0-3.el7.x86_64
```
## Install a RPM Package Without Dependencies
```
rpm -ivh --nodeps
```
sudo systemctl start docker

----------------------------------
## Give everyone read/execute access to your $HOME `To copy from home folder`
```
chmod a+rx ~/
```




