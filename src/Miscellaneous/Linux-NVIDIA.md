
```
yum install http://developer.download.nvidia.com/compute/cuda/repos/rhel8/x86_64/cuda-repo-rhel8-10.2.89-1.x86_64.rpm 
```

[Disabling Nouveau](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#runfile-nouveau)
```
echo 'blacklist nouveau
options nouveau modeset=0' > /etc/modprobe.d/blacklist-nouveau.conf  
dracut --force
#lsmod | grep nouveau

grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
```  

[Device Node Verification](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#runfile-verifications)  
```
yum install nvidia-driver
# cd /usr/src/460.32.03
# dkms install nvidia/460.32.03
rm /etc/X11/xorg.conf.d/10-nvidia.conf # We should delete this file otherwise the X server can't start up

yum install nvidia-modprobe
modprobe nvidia
modprobe nvidia-uvm
nvidia-modprobe
```

[PRIME Render Offload](http://download.nvidia.com/XFree86/Linux-x86_64/460.32.03/README/primerenderoffload.html)  
[Using PRIME render offload](https://wiki.archlinux.org/index.php/NVIDIA_Optimus#Using_PRIME_render_offload)  
[nvidia-prime](https://github.com/archlinux/svntogit-packages/tree/packages/nvidia-prime/trunk)  
[nvidia-utils](https://github.com/archlinux/svntogit-packages/tree/packages/nvidia-utils/trunk)  
```
rm /etc/X11/xorg.conf.d/10-nvidia.conf # We should delete this file otherwise the X server can't start up

echo 'Section "OutputClass"
    Identifier "nvidia"
    MatchDriver "nvidia-drm"
    Driver "nvidia"
    Option "AllowEmptyInitialConfiguration"
EndSection' > /etc/X11/xorg.conf.d/10-nvidia.conf  

# restart X server
# xrandr --listproviders # "NVIDIA-G0" should be listed

export __NV_PRIME_RENDER_OFFLOAD=1
export __GLX_VENDOR_LIBRARY_NAME=nvidia
glxinfo | grep NVIDIA
steam.sh
```

[Install plugins using Eclipse IDE](https://docs.nvidia.com/cuda/nsightee-plugins-install-guide/index.html#install-steps)  
[Importing CUDA Samples](https://docs.nvidia.com/cuda/nsight-eclipse-plugins-guide/index.html#import-sample)

