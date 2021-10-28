# Proxy Server 

You may rent the CentOS 8 machine by the Vultr / Alibaba Cloud and setup the proxy server by the following tutorial.  

## 1\.setup socks5 proxy 

### 1-1\.server side 
```bash
## do nothing
```

### 1-2\.client side 

```bash
ssh -f -N -T -M -D 9050 root@x.x.x.x ## dynamic port forwarding

google-chrome --proxy-server="socks5://localhost:9050" & disown ## use socks5 proxy
```
 
## 2\.setup http proxy

### 2-1\.server side 

```bash
yum install epel-release
yum update

# enable automatic update 
yum install dnf-automatic
systemctl enable dnf-automatic-install.timer
systemctl restart dnf-automatic-install.timer
# systemctl status dnf-automatic-install.timer

# install privoxy
yum install privoxy
vi /etc/privoxy/config
## -- listen-address  127.0.0.1:8118
## ++ listen-address  127.0.0.1:8118
systemctl enable privoxy
systemctl restart privoxy
## systemctl status privoxy
```

### 2-2\.client side - Linux/MacOS/Windows

```bash
ssh -f -N -T -M -L 8118:localhost:8118 root@x.x.x.x ## local port forwarding

google-chrome --proxy-server="http://localhost:8118" & disown ## use http proxy
```

### 2-3\.client side - Android  

Set the http proxy to "127.0.0.1:8118" by [Android Help / Set up a proxy to connect phones](https://support.google.com/android/answer/9654714?hl=en#zippy=%2Cset-up-a-proxy-to-connect-phones)  

### 2-3-1\.ConnectBot  
Use the "SSH client [ConnectBot](https://play.google.com/store/apps/details?id=org.connectbot)" to setup the "local port forwarding"  

### 2-3-2\.ADB

Use the "ADB [Reverse](https://android.googlesource.com/platform/system/adb/+/master/SERVICES.TXT)" to setup the "reverse forwaring"  
  
```bash
adb reverse tcp:8118 tcp:8080 ## adb reverse forwarding  

ssh -f -N -T -M -L8080:localhost:8118 ## local port forwarding  
```  