
```
curl -L -o /etc/yum.repos.d/cuda-rhel8.repo 'http://developer.download.nvidia.com/compute/cuda/repos/rhel8/x86_64/cuda-rhel8.repo'  
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
```

[PRIME Render Offload](http://download.nvidia.com/XFree86/Linux-x86_64/460.32.03/README/primerenderoffload.html)

```
export __NV_PRIME_RENDER_OFFLOAD=1
export __GLX_VENDOR_LIBRARY_NAME=nvidia
glxinfo
```