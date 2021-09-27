# How to use X11 forwarding for graphical applications from remote server to local computer
## Motivation
Utilize graphical applications from the remote server and view them at local machine. For instance, running programs remotely on server (using vscode) but still be able to visualize the matplotlib plots locally.
This is more stable than using interative windows such as IPython or jupyter notebooks. This might be the simplest way to do. I have tried using Gtk3Agg backend of Matplotlib etc but it is not working because of the source code configuration.

## How to do it
General pipeline:
1. Install X11 forwarding related softwares on server.
2. Install X11 forwarding related softwares on local computer.
3. Configure sshd_config and ssh_config on server.
4. Configure sshd_config and ssh_config on local computer.
5. Set display address using local computer address.

## An example
### Environment
Server: WSL2 (Windows Subsystem for Linux 2) 
Local: MacOS

### Step 1: Install X11 forwarding related softwares on server
useful link: https://www.youtube.com/watch?v=4SZXbl9KVsw
1. Install [VcSsrv Windows X Server](https://sourceforge.net/projects/vcxsrv/) and follow the default settings.
2. Allow administrator access if popped up.
3. Launch the XLaunch app on desktop and allow "Disable access control" in "Extra settings". Follow defualts for others.
4. Allow "Public networks" for firewall.

### Step 2: Install X11 forwarding related softwares on local machine
useful link: https://www.cyberciti.biz/faq/apple-osx-mountain-lion-mavericks-install-xquartz-server/
1. Install [XQuanrtz](https://www.xquartz.org) on mac 
2. Reboot the computer.

### Step 3: Configure sshd_config and ssh_config on server
1. Make sure that "X11Forwarding yes" and other X11 related settings are allowed in sshd_config
```
sudo nano /etc/ssh/sshd_config
```
uncomment or add the setting if necessary. Usually just check all X11 related settings are allowed.
2. Again, make sure all X11 related settings are allowed at local machine,
```
sudo nano /etc/ssh/ssh_config
```
and check all related settings. This should be done on WSL2 terminal.

### Step 4: Configure sshd_config and sshd_config at local machine
Repeat step 3 at mac terminal.

### Step 5: Set display address using local computer address
1. Get display addresses of server and local machine
  - Server (IP address)
  ```
  hostname -I
  ```
  or
  ```
  ip addr show
  ```
  - Local machine (this might not be your IP address, usually is 127.0.0.1)!!!
  ```
  nano /etc/hosts
  ```
  
3. Configure the display address (the address you want the applications/plots to display)
  - If it is on server (WSL2):
  ```
  export DISPLAY={YOUR_DISPLAY_ADDRESS}:0.0
  ```
  this is because Windows uses IP_address:0.0 as the defualt.
  - If it is at local machine (MacOS):
  ```
  export DISPLAY={YOUR_DISPLAY_ADDRESS}:10.0
  ```
  this is because MacOS uses IP_address:10.0
  - Set LIBGL_ALWAYS_INDIRECT variable
  ```
  export LIBGL_ALWAYS_INDIRECT=1
  ```

### Test
1. SSH your server
2. Configure the display address
3. Check a simple application
```
xeyes
```
You should see an eye popped up at your local machine.

## Troubleshooting
1. Error: Can't open display: X.X.X.X:10:0

Solution: Your display address is not configured correctly. Check whether X11 are given access in the files. Check DISPLAY variable using
```
echo $DISPLAY
```
