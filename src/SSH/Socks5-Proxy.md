## Socks5 Proxy

You may rent the CentOS 8 machine by the Vultr / Alibaba Cloud and use the sock5 proxy by the following tutorial.  

### 1\.dynamic port forwarding  
```
ssh -D 1080 root@x.x.x.x ## start the sock5 proxy to listen on the port 1080
```

### 2\.socks5 proxy
```
google-chrome --proxy-server="socks5://localhost:1080" & disown ## configuring a socks5 proxy server in chrome
```
