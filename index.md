


# miscellaneous  

## Linux Bluetooth  

### ORICO BTA-508  

dmesg output  
```  
Bluetooth: hci0: RTL: firmware file rtl_bt/rtl8761b_fw.bin not found  
```

download the rtl8761b_fw from https://github.com/Realtek-OpenSource/android_hardware_realtek/blob/rtk1395/bt/rtkbt/Firmware/BT/rtl8761b_fw   
move the downloaded rtl8761b_fw to /usr/lib/firmware/rtl_bt/rtl8761b_fw.bin  