## Socks5 Proxy

You may rent the CentOS 8 machine by the Vultr / Alibaba Cloud and use the sock5 proxy by the following tutorial.  

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