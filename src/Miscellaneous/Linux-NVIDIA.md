
```
yum install http://developer.download.nvidia.com/compute/cuda/repos/rhel8/x86_64/cuda-repo-rhel8-10.2.89-1.x86_64.rpm 
```

[Disabling Nouveau](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#runfile-nouveau)
```
echo 'blacklist nouveau
options nouveau modeset=0' > /etc/modprobe.d/blacklist-nouveau.conf  
dracut --force
grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
#lsmod | grep nouveau
```  

[Device Node Verification](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#runfile-verifications)  
```
yum install nvidia-driver
#cd /usr/src/460.32.03
dkms install nvidia/460.32.03
modprobe nvidia
modprobe nvidia-uvm
```

[PRIME Render Offload](http://download.nvidia.com/XFree86/Linux-x86_64/460.32.03/README/primerenderoffload.html)

```
export __NV_PRIME_RENDER_OFFLOAD=1
export __GLX_VENDOR_LIBRARY_NAME=nvidia
glxinfo
```

[Install plugins using Eclipse IDE](https://docs.nvidia.com/cuda/nsightee-plugins-install-guide/index.html#install-steps)  
[Importing CUDA Samples](https://docs.nvidia.com/cuda/nsight-eclipse-plugins-guide/index.html#import-sample)

