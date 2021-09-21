# how to set up ssh on Ubuntu Windows subsystem (WSL)
useful link: https://www.illuminiastudios.com/dev-diaries/ssh-on-windows-subsystem-for-linux/
useful link: https://phoenixnap.com/kb/ssh-permission-denied-publickey

## Important!!!
There are two ways to enable openssh-server: 1) Windows Subsystem for Linux (WSL) 2) Windows openssh (installed using powershell or through settings->App->Optional features. They will conflict if you have both!!! So have one of them and remove the others. Highly recommend installing through WSL. If you have installed Windows openssh, uninstall it through settings->App->Optional features and reboot the computer following the instruction. Usually, there is no need to change the sshd_config file. 

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
check hostname:
```
hostname -I
```
check ip address: 
```
ip addr show
```
