[CPU frequency driver](https://wiki.archlinux.org/title/CPU_frequency_scaling#CPU_frequency_driver)  
```bash
vi /etc/default/grub
-- GRUB_CMDLINE_LINUX_DEFAULT=""
++ GRUB_CMDLINE_LINUX_DEFAULT="intel_pstate=disable"

## Debian
update-grub

## CentOS
grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg

## reboot
```

[Scaling governors](https://wiki.archlinux.org/title/CPU_frequency_scaling#Scaling_governors)  
```bash
for i in {0..31}; do echo schedutil > /sys/devices/system/cpu/cpu${i}/cpufreq/scaling_governor; done
# for i in {0..31}; do cat /sys/devices/system/cpu/cpu${i}/cpufreq/scaling_governor; done
```