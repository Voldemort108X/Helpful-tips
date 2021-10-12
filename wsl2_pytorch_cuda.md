# How to install Pytorch with Nvidia CUDA on WSL2
## Prerequisite:
1. CUDA is only supported on WSL2, check out https://docs.nvidia.com/cuda/wsl-user-guide/index.html for detailed version support
2. CUDA GPU access is only supported in Windows Insider Build, check out https://christianjmills.com/Using-PyTorch-with-CUDA-on-WSL2/ for enrollment. Enroll and update your Windows to the latest developer version.

## Steps
1. (Optional) Upgrade your WSL1 to WSL2. Follow the instructions at https://docs.microsoft.com/en-us/windows/wsl/install-manual until step 5 or 6, depending on your previous WSL configuration. Then, type the following to start conversion, which will take a few minutes.
```
wsl --set-version Ubuntu 2
```
2. Follow the steps in https://docs.nvidia.com/cuda/wsl-user-guide/index.html. The only thing you need to download and install from the website is the driver. Other configuration should be good to go using command lines.
3. Enroll the windows insider build program. The current build (Build 22417, at Oct. 11, 2021) supports CUDA on WSL2. Make sure you update the build version that supports WSL2. This is _very important_ and can be tested using nvidia-smi or torch.cuda.is_available().

## Status check command
1. Check your WSL kernel version (recommend 5.10.16.3 or later). Open a windows CMD, and type
```
uname -r
```
and check whether it is WSL or WSL2
```
wsl -l -v
```
2. Check your CUDA status. Open a Windows cmd and type
```
wsl
```
and then type
```
nvidia-smi
```
or
```
import torch
torch.cuda.is_available()
```
If nvidia-smi command gives some info or cuda.is_available() function returns True, the setup is good to go.
