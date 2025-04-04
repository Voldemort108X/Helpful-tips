# how to set up ssh on Ubuntu Windows subsystem (WSL)
useful link: https://www.illuminiastudios.com/dev-diaries/ssh-on-windows-subsystem-for-linux/
useful link: https://phoenixnap.com/kb/ssh-permission-denied-publickey

## 0322 Update
1. After a random windows update, the IPhelper service is not running automatically. The dependency of it has been changed. Thus, the ```netsh``` command to do port forwarding is invalid.
2. To solve this, we need to delete the potentially deprecated dependency and force it to start:
## 🛠 Fix IP Helper Error 1075: Restore `DependOnService`

### 📍 Step 1: Open the Registry Editor

1. Press `Win + R`, type `regedit`, and press **Enter**.
2. In the Registry Editor, navigate to:

   ```
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\iphlpsvc
   ```

3. In the right pane, locate the entry named `DependOnService`.

   - If it's missing, incorrect, or contains junk values — it needs to be fixed.

---

### 🔧 Step 2: Set `DependOnService` to the Required Value

1. Double-click `DependOnService` to edit it.
2. Set it to this **multi-string** value:

   ```
   RpcSs
   ```

   - Press **Enter** after typing `RpcSs` so it appears as a new line in the editor.
   - Make sure it’s the **only** entry listed.

3. Click **OK** to save the changes.

---

### 🔁 Step 3: Restart Your Computer

Restart your Windows machine to apply the changes.

---

### ✅ Step 4: Start the IP Helper Service

1. Press `Win + R`, type `services.msc`, and press **Enter**.
2. Locate **IP Helper** in the list.
3. Right-click → **Start**

You should no longer see **Error 1075**, and the IP Helper service should be running properly.



## TODO:
Run WSL2 script automatically after restart.

## WSL location
C:\Users\Xiaoran Zhang\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs\home\xiaoranzhang\miniconda3

## WSL2 ip 
WSL2 uses a dynamic ip address and thus can be annoying to connect. Find the windows address using  WSL2 ip address using hostname -I and add the following to the Windows powershell terminal as administrator (replace {YOUR_WINDOWS_IP_ADDRESS} or {YOUR_WSL2_IP_ADDRESS} with the actual ip)
```
netsh interface portproxy add v4tov4 listenport=22 listenaddress={YOUR_WINDOWS_IP_ADDRESS} connectport=22 connectaddress={YOUR_WSL2_IP_ADDRESS}
```
or the following command which helpes you to automatically detect the ip address
```
netsh interface portproxy add v4tov4 listenport=22 listenaddress={YOUR_WINDOWS_IP_ADDRESS} connectport=22 connectaddress=(wsl hostname -I).trim()
```

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

## Steps to install anaconda on WSL Ubuntu terminal (please stricly follow this to avoid usage issues
Original link: https://gist.github.com/kauffmanes/5e74916617f9993bc3479f401dfec7da

1. Install WSL (Ubuntu for Windows - can be found in Windows Store). I recommend the latest version (I'm using 18.04) because there are some bugs they worked out during 14/16 (https://github.com/Microsoft/WSL/issues/785)
2. Go to https://repo.continuum.io/archive to find the list of Anaconda releases
3. Select the release you want. I have a 64-bit computer, so I chose the latest release ending in `x86_64.sh`. If I had a 32-bit computer, I'd select the `x86.sh` version. If you accidentally try to install the wrong one, you'll get a warning in the terminal. I chose `Anaconda3-5.2.0-Linux-x86_64.sh`.
4. From the terminal run `wget https://repo.continuum.io/archive/[YOUR VERSION]`. Example: `$ wget https://repo.continuum.io/archive/Anaconda3-5.2.0-Linux-x86_64.sh`
5. Run the installation script: `$ bash Anaconda[YOUR VERSION].sh` (`$ bash Anaconda3-5.2.0-Linux-x86_64.sh`)
6. Read the license agreement and follow the prompts to accept. When asks you if you'd like the installer to prepend it to the path, say yes.
7. Optionally install VS Code when prompted (some have reported this installation doesn't work - checkout https://gist.github.com/kauffmanes/5e74916617f9993bc3479f401dfec7da#gistcomment-3665550)
8. Close the terminal and reopen it to reload .bash configs.
9. To test that it worked, run `$ which python`. It should print a path that has anaconda in it. Mine is `/home/kauff/anaconda3/bin/python`. If it doesn't have anaconda in the path, do the next step. Otherwise, move to step 11.
10. Manually add the Anaconda bin folder to your PATH. To do this, I added "export PATH=/home/kauff/anaconda3/bin:$PATH" to the bottom of my ~/.bashrc file. 
11. To open jupyter, type `$ jupyter notebook --no-browser`. The no browser flag will still run Jupyter on port 8888, but it won't pop it open automatically. it's necessary since you don't have a browser (probably) in your subsystem. In the terminal, it will give you a link to paste into your browser. If it worked, you should see your notebooks!
