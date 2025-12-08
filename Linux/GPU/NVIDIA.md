[NVIDIA - Disabling Nouveau](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#runfile-nouveau)
```bash
# CentOS
echo 'blacklist nouveau' > /etc/modprobe.d/blacklist-nouveau.conf
echo 'options nouveau modeset=0' >> /etc/modprobe.d/blacklist-nouveau.conf  
dracut --force
grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg  

# Debian
echo 'blacklist nouveau' > /etc/modprobe.d/blacklist-nouveau.conf
echo 'options nouveau modeset=0' >> /etc/modprobe.d/blacklist-nouveau.conf
update-initramfs -u
update-grub

# Ubuntu
echo 'blacklist nouveau' > /etc/modprobe.d/blacklist-nouveau.conf
echo 'options nouveau modeset=0' >> /etc/modprobe.d/blacklist-nouveau.conf
update-initramfs -u
update-grub

lsmod | grep nouveau
```  

[Arch Linux - NVIDIA](https://wiki.archlinux.org/title/NVIDIA)  
[NVIDIA - Modesetting](https://download.nvidia.com/XFree86/Linux-x86_64/555.58.02/README/kms.html)  
```bash

# Nvidia modesetting support. 
# Set to 0 or comment to disable kernel modesetting support. 
# This must be disabled in case of Mosaic or SLI.

# CentOS
echo 'options nvidia-drm modeset=0 fbdev=0' > /etc/modprobe.d/nvidia-modeset.conf
echo 'options nvidia NVreg_DynamicPowerManagement=0x02' > /etc/modprobe.d/nvidia-power-management.conf
dracut --force
grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg  

cat /sys/module/nvidia_drm/parameters/modeset
```

[NVIDIA - Persistence Daemon](https://docs.nvidia.com/deploy/driver-persistence/index.html#persistence-daemon)  
```bash
nvidia-persistenced --user HanetakaChou  
# systemctl status nvidia-persistenced

# nvidia-smi -pm 1
# nvidia-smi -pm 0
```

[NVIDIA - Package Manager Installation](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#package-manager-installation)  
```bash
# CentOS
# https://developer.download.nvidia.com/compute/cuda/repos/rhel9/x86_64/cuda-rhel9.repo

# Debian
apt install https://developer.download.nvidia.com/compute/cuda/repos/debian11/x86_64/cuda-keyring_1.0-1_all.deb

# Ubuntu
apt install https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.0-1_all.deb

```  

[NVIDIA - Open Kernel Modules](https://docs.nvidia.com/datacenter/tesla/driver-installation-guide/index.html#open-kernel-modules)  
[NVIDIA - Meta Packages](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#meta-packages)  
```bash
# CentOS
yum module reset nvidia-driver
yum module install nvidia-driver:555-dkms
# yum module install nvidia-driver:latest-dkms
# yum module install nvidia-driver:560-open
# yum module install nvidia-driver:open-dkms

yum install nvidia-driver-libs.i686

# yum install cuda-runtime-12-5
yum install cuda-runtime-12-9

yum install libcudnn9-cuda-12

# cd /usr/src/nvidia-555.42.06
# dkms install nvidia/555.42.06

# Debian
apt install nvidia-driver
apt install libgl1-nvidia-glvnd-glx
apt install libgl1-nvidia-glvnd-glx:i386  
apt install nvidia-vulkan-icd
apt install nvidia-vulkan-icd:i386  

# Ubuntu
apt install nvidia-driver-520
apt install libnvidia-gl-520
apt install libnvidia-gl-520:i386
```

[Arch Linux - NVIDIA Optimus](https://wiki.archlinux.org/index.php/NVIDIA_Optimus#Using_PRIME_render_offload)  
[Arch Linux - PRIME](https://wiki.archlinux.org/title/PRIME#PRIME_render_offload)  
[NVIDIA - PRIME Render Offload](https://download.nvidia.com/XFree86/Linux-x86_64/435.17/README/primerenderoffload.html)  
[Arch Linux - prime run](https://github.com/archlinux/svntogit-packages/blob/packages/nvidia-prime/trunk/prime-run)  
[Arch Linux - NVIDIA](https://wiki.archlinux.org/title/NVIDIA)  
```bash
# CentOS

# We should replace the configuration file otherwise the X can NOT start up  

# We may simply delete 
# rm /etc/X11/xorg.conf.d/10-nvidia.conf  

# Or we may comment out the 'Option "PrimaryGPU" "yes"'
vi /etc/X11/xorg.conf.d/10-nvidia.conf  
# ...
# 
# Section "OutputClass"
# ...
#    # Option "PrimaryGPU" "yes"
# ... 

# reboot
xrandr --listproviders | grep 'NVIDIA-G0'

env __NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia glxinfo
env __NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia steam & disown

nvidia-smi

export TF_CPP_MIN_LOG_LEVEL=0
export TF_CPP_MAX_VLOG_LEVEL=3
python -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
```
