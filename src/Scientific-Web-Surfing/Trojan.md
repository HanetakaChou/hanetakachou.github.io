# Trojan  

You may rent the CentOS 8 machine by the Vultr / Alibaba Cloud and deploy your own Trojan by the following tutorial.

## 1\. server side  

### 1-1\. config CentOS server
```bash
# change to Minimal Server
yum group install 'Minimal Server'
rpm -e --nodeps sudo
yum group remove 'Server'

# add epel repo
yum install epel-release
yum update

# enable automatic update 
yum install dnf-automatic
systemctl enable dnf-automatic-install.timer
systemctl restart dnf-automatic-install.timer
# systemctl status dnf-automatic-install.timer
```
### 1-2\. deploy Nginx server
```bash
yum install nginx

# firewall-cmd --info-service=http
firewall-cmd --add-service http ## --zone=public
# firewall-cmd --list-services ## --zone=public
firewall-cmd --add-masquerade ## --zone=public
#  ## --zone=public
firewall-cmd --runtime-to-permanent
firewall-cmd --reload

# you may change '/etc/nginx/nginx.conf' and '/usr/share/nginx/html/index.html' to your personalize content

systemctl enable nginx
systemctl restart nginx
# systemctl status nginx
```

### 1-3\. generate TLS cert

```bash
mkdir -p /etc/pki/nginx
mkdir -p /etc/pki/nginx/private

# generate key
openssl genrsa -des3 -out /etc/pki/nginx/private/server.key 2048

# remove key password
openssl rsa -in /etc/pki/nginx/private/server.key -out /etc/pki/nginx/private/server.key

# generate cert
openssl req -new -x509 -key /etc/pki/nginx/private/server.key -out tmp-server.crt -days 7777
openssl req -new -key /etc/pki/nginx/private/server.key -out tmp-server.csr
openssl x509 -req -days 7777 -in tmp-server.csr -CA tmp-server.crt -CAkey /etc/pki/nginx/private/server.key -CAcreateserial -out /etc/pki/nginx/server.crt
rm tmp-server.crt
rm tmp-server.csr

# TODO: certbot
# yum install certbot
```

### 1-4\. deploy Trojan server

```bash
# https://github.com/trojan-gfw/trojan/wiki/Binary-&-Package-Distributions
curl -o ./trojan-quickstart.sh -fsSL https://raw.githubusercontent.com/trojan-gfw/trojan-quickstart/master/trojan-quickstart.sh
chmod +X ./trojan-quickstart.sh
./trojan-quickstart.sh

vi /usr/local/etc/trojan/config.json
- "password1",
- "password2"
+ "YourPrivatePassword"
- "cert": "/path/to/certificate.crt"
+ "cert": "/etc/pki/nginx/server.crt"
- "key": "/path/to/private.key"
+ "key": "/etc/pki/nginx/private/server.key"


# firewall-cmd --info-service=https
firewall-cmd --add-service https ## --zone=public
# firewall-cmd --list-services ## --zone=public
firewall-cmd --add-masquerade ## --zone=public
#  ## --zone=public
firewall-cmd --runtime-to-permanent
firewall-cmd --reload

systemctl enable trojan
systemctl restart trojan
# systemctl status trojan
```

## 2\.client side - Linux/MacOS/Windows

```bash
download https://github.com/trojan-gfw/trojan/releases  

edit config.json
- "local_port": 1080
+ "local_port": 9050 # follow the convention of Tor
- "remote_addr": "example.com"
+ "remote_addr": "YourPrivateAddress"
- "password1"
+ "YourPrivatePassword"
- "verify": true
+ "verify": false
- "verify_hostname": true 
+ "verify_hostname": false

execute trojan # cd to the trojan directory

google-chrome --proxy-server="socks5://localhost:9050" & disown # use socks5 proxy

# TODO: you may use privoxy to forward the http proxy to the socks5 proxy  
```

## 3\.client side - Android

```bash
download https://github.com/Kr328/ClashForAndroid/releases

# https://v2xtls.org/clash-for-android%e9%85%8d%e7%bd%aetrojan%e6%95%99%e7%a8%8b/
https://v2xtls.org/clash_template2.yaml

edit clash_template2.yaml
type: trojan
- server: server
+ server: YourPrivateAddress
- password: password
+ password: YourPrivatePassword
+ skip-cert-verify: true
```