

mkdir -p ~/.ssh
chmod 700 ~/.ssh
 Generate a new key pair in Linux


### Copy the public half of the key pair to your cloud server
```
ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
```
This also assumes you saved the key pair using the default file name and location. If not, just replace the key path ~/.ssh/id_rsa.pub above with your own key name.

` (Optional) Set up SSH Agent to store the keys to avoid having to re-enter passphrase at every login
```
ssh-agent $BASH
ssh-add ~/.ssh/id_rsa
```
## Using PuTTY
```
sudo nano authorized_keys
```
Paste the public key into the file 
or read the uploaded public key and append
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

ref:
https://www.ssh.com/ssh/putty/putty-manuals/0.68/Chapter8.html
