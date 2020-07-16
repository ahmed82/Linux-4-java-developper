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
