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

# lsmod | grep nouveau
```  

[NVIDIA - Package Manager Installation](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#package-manager-installation)  
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

env __NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia glxinfo
env __NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia steam & disown

# yum install nvidia-driver-cuda
# nvidia-smi
```

[Arch Linux - Hardware Video Acceleration](https://wiki.archlinux.org/title/Hardware_video_acceleration#Translation_layers)  
[Arch Linux - NVIDIA](https://wiki.archlinux.org/title/NVIDIA#DRM_kernel_mode_setting)  
[Debian - Hardware Video Acceleration](https://wiki.debian.org/HardwareVideoAcceleration#NVENC.2FNVDEC)  
[Chromium - VA-API](https://chromium.googlesource.com/chromium/src/+/master/docs/gpu/vaapi.md#VaAPI-on-Linux)  
```bash

# A VDPAU-based backend for VA-API 

# CentOS
# yum install libva-vdpau-driver
# yum install nvidia-driver-libs

# Debian
# apt install vdpau-va-driver
# apt install vdpau-va-driver:i386
# apt install libvdpau-va-gl1
# apt install libvdpau-va-gl1:i386
# apt install nvidia-vdpau-driver
# apt install nvidia-vdpau-driver:i386

# Ubuntu
# apt install vdpau-va-driver
# apt install vdpau-va-driver:i386
# apt install nvidia-driver-520

# A CUDA NVDECODE based backend for VA-API

# CentOS
yum install nvidia-vaapi-driver 

# Debian
apt install nvidia-vaapi-driver
apt install libcuda1
apt install libcuda1:i386
apt install libnvcuvid1
apt install libnvcuvid1:i386
apt install libnvidia-encode1
apt install libnvidia-encode1:i386
apt install libavcodec-extra58

# Ubuntu
apt install nvidia-vaapi-driver

# DRM kernel mode setting

vi /etc/default/grub
-- GRUB_CMDLINE_LINUX_DEFAULT=""
++ GRUB_CMDLINE_LINUX_DEFAULT="nvidia-drm.modeset=1"

## Debian
update-grub

## CentOS
grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg

## reboot

# Verify VA-API

# yum install libva-utils
# apt install vainfo
env __NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia LIBVA_DRIVER_NAME=nvidia NVD_LOG=1 vainfo

env __NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia LIBVA_DRIVER_NAME=nvidia NVD_LOG=1 mpv --hwdec=vaapi --player-operation-mode=pseudo-gui & disown

env __NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia LIBVA_DRIVER_NAME=nvidia google-chrome-stable --enable-features=VaapiVideoDecoder --ignore-gpu-blocklist --use-gl=egl & disown
```

[NVIDIA - Install plugins using Eclipse IDE](https://docs.nvidia.com/cuda/nsightee-plugins-install-guide/index.html#install-steps)  
[NVIDIA - Importing CUDA Samples](https://docs.nvidia.com/cuda/nsight-eclipse-plugins-guide/index.html#import-sample)

