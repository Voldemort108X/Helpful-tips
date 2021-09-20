# how to set up ssh on Ubuntu Windows subsystem (WSL)
useful link: https://www.illuminiastudios.com/dev-diaries/ssh-on-windows-subsystem-for-linux/
useful link: https://phoenixnap.com/kb/ssh-permission-denied-publickey
## Prerequisite:
1. Enable Linux on windows subsystem: https://www.ssl.com/how-to/enable-linux-subsystem-install-ubuntu-windows-10/
2. Download Ubuntu from windows

## Install ssh
```
sudo apt remove openssh-server
sudo apt install openssh-server
```

## Edit sshd_config (enable password login instead of publickey)
```
sudo nano /etc/ssh/sshd_config
```
change password authentication to yes

## Restart/ Start ssh service
```
service ssh status
```
if it is not runing then type
```
sudo service ssh start
```
if it is runing then type
```
sudo service ssh --full-restart
```

## Test your connection
check ip address: 
```
ip addr show
```
