# setup ssh key for no user/password
## on Linux box:
```
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```
Generate a new key pair in Linux
```
ssh-keygen -t rsa -b 4096
```

# Move the public key to .ssh/authorized_keys file.
```
cat .ssh/id_rsa.pub >> .ssh/authorized_keys
```
` Make sure to append the key (‘>>’), otherwise existing keys in the authorized_keys will be deleted.

This also assumes you saved the key pair using the default file name and location. If not, just replace the key path ~/.ssh/id_rsa.pub above with your own key name.
### Copy the public half of the key pair to your cloud server
```
ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
or just 
ssh-copy-id user@server / type remote password one last time.
```


### (Optional) Set up SSH Agent to store the keys to avoid having to re-enter passphrase at every login
```
ssh-agent $BASH
ssh-add ~/.ssh/id_rsa
```
## Using PuTTY
```
sudo vi authorized_keys
```
Paste the public key into the file 
or read the uploaded public key and append as the command below:
```
[server]$ ssh-keygen -i -f localpubkey >> ~/.ssh/authorized_keys
```
select the public key in putty configuration box, click 'Connection' > 'SSH > Auth'.
Add username  'Connection > Data' then in the first field which is named 'Auto-login' username.

## Turn off password authentication
```
PasswordAuthentication no
sudo nano /etc/ssh/sshd_config
PubkeyAuthentication yes
sudo systemctl restart sshd
```
# Windows
## ssh from windows
```
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'
```
if not installed
```
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
```
Start-Service sshd
Get-Service sshd
Set-Service -Name sshd -StartupType 'Automatic'
Get-NetFirewallRule -Name *ssh*

ref:
https://www.ssh.com/ssh/putty/putty-manuals/0.68/Chapter8.html
