## Proxy Server 

You may rent the CentOS 8 machine by the Vultr / Alibaba Cloud and setup the proxy server by the following tutorial.  

### 1\.setup socks5 proxy 
```
ssh -D 9050 root@x.x.x.x ## dynamic port forwarding
```

### 2\.use socks5 proxy
```
google-chrome --proxy-server="socks5://localhost:9050" & disown
```
 
### 3\.setup http proxy (optional)
```
yum install privoxy

vi /etc/privoxy/config
-- listen-address  127.0.0.1:8118
++ listen-address  127.0.0.1:8118
++ forward-socks5 / localhost:9050 .

systemctl restart privoxy
```

### 4\.use http proxy (optional)
```
google-chrome --proxy-server="http://localhost:8118" & disown
```

### Appendix  

setup the proxy server on any PC in the local network
```
vi /etc/privoxy/config
-- listen-address  127.0.0.1:8118
++ listen-address  0.0.0.0:8118

# firewall-cmd --info-service=privoxy
firewall-cmd --add-service privoxy ## --zone=public
# firewall-cmd --list-services ## --zone=public
firewall-cmd --add-masquerade ## --zone=public
#  ## --zone=public
firewall-cmd --runtime-to-permanent
firewall-cmd --reload

# ifconfig
# e.g 192.168.0.108
```

[Android Help / Set up a proxy to connect phones](https://support.google.com/android/answer/9654714?hl=en#zippy=%2Cset-up-a-proxy-to-connect-phones)  
The "Host Name" should be the PC in the local network # e.g 192.168.0.108  


