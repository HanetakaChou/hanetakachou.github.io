[Disabling Nouveau](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#runfile-nouveau)
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

# lsmod | grep nouveau
```  

[Package Manager Installation](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#package-manager-installation)  
```bash
# CentOS
yum install http://developer.download.nvidia.com/compute/cuda/repos/rhel8/x86_64/cuda-repo-rhel8-10.2.89-1.x86_64.rpm 

# Debian
apt install https://developer.download.nvidia.com/compute/cuda/repos/debian11/x86_64/cuda-keyring_1.0-1_all.deb

# Ubuntu
apt install https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.0-1_all.deb

```  

```bash
# CentOS
yum install nvidia-driver
# cd /usr/src/520.61.05
# dkms install nvidia/520.61.05

# Debian
apt install libgl1-nvidia-glvnd-glx
apt install libgl1-nvidia-glvnd-glx:i386  

# Ubuntu
apt install nvidia-driver-520
apt install libnvidia-gl-520
apt install libnvidia-gl-520:i386
```

[PRIME Render Offload](http://download.nvidia.com/XFree86/Linux-x86_64/460.32.03/README/primerenderoffload.html)  
[Using PRIME render offload](https://wiki.archlinux.org/index.php/NVIDIA_Optimus#Using_PRIME_render_offload)  
[nvidia-prime](https://github.com/archlinux/svntogit-packages/tree/packages/nvidia-prime/trunk)  
[nvidia-utils](https://github.com/archlinux/svntogit-packages/tree/packages/nvidia-utils/trunk)  
```bash
# CentOS

# We should replace this file otherwise the X can NOT start up.  
# rm /etc/X11/xorg.conf.d/10-nvidia.conf 
echo 'Section "OutputClass"' > /etc/X11/xorg.conf.d/10-nvidia.conf 
echo '    Identifier "nvidia"' >> /etc/X11/xorg.conf.d/10-nvidia.conf
echo '    MatchDriver "nvidia-drm"' >> /etc/X11/xorg.conf.d/10-nvidia.conf
echo '    Driver "nvidia" >> /etc/X11/xorg.conf.d/10-nvidia.conf
echo '    Option "AllowEmptyInitialConfiguration" >> /etc/X11/xorg.conf.d/10-nvidia.conf
echo 'EndSection' >> /etc/X11/xorg.conf.d/10-nvidia.conf  

# reboot
# xrandr --listproviders | grep 'NVIDIA-G0'

export __NV_PRIME_RENDER_OFFLOAD=1
# export __NV_PRIME_RENDER_OFFLOAD_PROVIDER=NVIDIA-G0
export __GLX_VENDOR_LIBRARY_NAME=nvidia
# export __VK_LAYER_NV_optimus=NVIDIA_only
glxinfo | grep NVIDIA
# glxgears
# vkcube
# steam.sh

# yum install nvidia-driver-cuda
# nvidia-smi
```

[Install plugins using Eclipse IDE](https://docs.nvidia.com/cuda/nsightee-plugins-install-guide/index.html#install-steps)  
[Importing CUDA Samples](https://docs.nvidia.com/cuda/nsight-eclipse-plugins-guide/index.html#import-sample)

