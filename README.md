## License  
```  
Copyright (C) YuqiaoZhang

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License along with this program.  If not, see <https://www.gnu.org/licenses/>
```  
   

## Scientific Textbooks

[Logic.md](Logic.md)  

### Analysis  
   
> [Analysis/1_Real_Analysis.md](Analysis/1_Real_Analysis.md)    

\[Pugh 2015\] Charles Pugh. "Real Mathematical Analysis, Second Edition." Springer 2015.  
\[Tu 2011\] Loring Tu. "An Introduction to Manifolds, Second Edition." Springer 2011.  

### Algebra  

> [Algebra/1_Linear_Algebra.md](Algebra/1_Linear_Algebra.md)   

\[Axler 2015\] Sheldon Axler. "Linear Algebra Done Right, Third edition." Springer 2015  

### Computer  

[Compiler.md](Compiler.md)  

## Scientific Web Browsing

### I\.Pritunl

You may rent the CentOS 8 machine by the Vultr and deploy your own VPN server by the following tutorial.

#### 1\.install Pritunl

##### server side  
```shell  
yum install epel-release
yum update

# https://docs.mongodb.com/manual/tutorial/install-mongodb-on-red-hat/
echo '[mongodb-org-4.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.4.asc' > /etc/yum.repos.d/mongodb-org-4.4.repo

yum install mongodb-org
systemctl enable mongod
systemctl restart mongod
# systemctl status mongod

# config the mongodb to only listen on localhost for security
# /etc/mongod.conf # bindIp 127.0.0.1

# https://docs.pritunl.com/docs/repo
echo '[pritunl]
name=Pritunl Repository
baseurl=https://repo.pritunl.com/stable/yum/centos/8/
gpgcheck=1
enabled=1' > /etc/yum.repos.d/pritunl.repo
gpg --keyserver hkp://keyserver.ubuntu.com --recv-keys 7568D9BB55FF9E5287D586017AE645C0CF8E292A
gpg --armor --export 7568D9BB55FF9E5287D586017AE645C0CF8E292A > key.tmp; rpm --import key.tmp; rm -f key.tmp

# https://docs.pritunl.com/docs/installation
yum install pritunl
systemctl enable pritunl
systemctl restart pritunl
# systemctl status pritunl

# https://docs.pritunl.com/docs/configuration-5  
ssh -L8080:localhost:443 root@x.x.x.x ## use ssh forwarding to tunnel through the firewall
# access the https://localhost:8080 by your web browser  
# fill the setup key with the output by the command "pritunl setup-key" and leave the MongoDB URI by default "mongodb"//localhost:27017/pritunl"

# yum install policycoreutils-gui ## sepolicy
# yum install policycoreutils-python-utils ## semanege
# ps -AZ | grep pritunl
# semanege fcontext -l | grep pritunl
# sepolicy network -a /usr/lib/pritunl/bin/pritunl
# pritunl is only allowed to bind on "unreserved" port 
# semanage port -l | grep 1194
# however the 1194/udp is "reserved" by openvpn_port_t
# semanage module -l | grep pritunl
# semanage module -l | grep openvpn

ssh -L8080:localhost:443 root@x.x.x.x ## use ssh forwarding to tunnel through the firewall
# access the https://localhost:8080 by your web browser
# fill the username with "pritunl" and password with the output by the command "pritunl default-password"
# add a server with "4911/udp" since the port "1194/udp" (compatible with the firewalld) is denied by the SELinux  ## firewall-cmd --info-service=openvpn ## semanage port -l | grep 4911
# add an organization and a user  
# attach the server to the organization and start the server

# config firewall
firewall-cmd --permanent --new-service=pritunl
firewall-cmd --permanent --service=pritunl --add-port=4911/udp
firewall-cmd --reload
# firewall-cmd --info-service=pritunl
firewall-cmd --add-service pritunl ## --zone=public
# firewall-cmd --list-services ## --zone=public
firewall-cmd --add-masquerade ## --zone=public
# firewall-cmd --query-masquerade ## --zone=public
firewall-cmd --runtime-to-permanent
firewall-cmd --reload
```

#### 2\.import OpenVPN profile

##### common
```shell
ssh -L8080:localhost:443 root@x.x.x.x ## use ssh forwarding to tunnel through the firewall
# access the https://localhost:8080 by your web browser
# fill the username with "pritunl" and password with the output by the command "pritunl default-password"
# download the user profile from the "Users" section (https://localhost:8080/#/users) 
# extract the "xxx.ovpn" from the downloaded tar file

# the following is the same as the OpenVPN Access Server
```

##### Windows/Mac/Android/IOS client
```shell
# download the openvpn client from the https://openvpn.net/download-open-vpn/ by your web browser 
```

##### Linux client  
```shell
# we don't need to download the client and we may use the "plasma-nm-openvpn"
nmcli connection import type openvpn file "path-to-the-client.ovpn" ## import the profile
```  

#### 3\.connect OpenVPN

##### Windows/Mac/Android/IOS client  
```shell
# connect to the imported profile by the client UI
```

##### Linux client  
```shell
# connect by the plasma-nm UI ##  leave the "(Private) key Password" blank
```

### II\.OpenVPN Access Server

You may rent the CentOS 8 machine by the Vultr and deploy your own VPN server by the following tutorial.  
The OpenVPN Access Server is free for a **maximum** of **two** simultaneous VPN connections and we recommend you deploy the Pritunl instead.

#### 1\.install OpenVPN Access Server

```shell  
yum install https://as-repository.openvpn.net/as-repo-centos8.rpm
yum install openvpn-as

# /usr/local/openvpn_as/bin/ovpn-init ## we may generate another new profile and leave the old one invalid from time to time for security
passwd openvpn ## set the password of the user "openvpn"

# config the web server to only listen on localhost for security
/usr/local/openvpn_as/scripts/sacli --key "cs.https.ip_address" --value "127.0.0.1" ConfigPut
/usr/local/openvpn_as/scripts/sacli --key "admin_ui.https.ip_address" --value "127.0.0.1" ConfigPut
/usr/local/openvpn_as/scripts/sacli start
systemctl restart openvpnas

# accept the Agreement
ssh -L8080:localhost:943 root@x.x.x.x ## use ssh forwarding to tunnel through the firewall
# access the https://localhost:8080/admin (with the "/admin") by your web browser  
# your web browser may warn the website is unsafe and we may ignore the warning
# login with the admin user "openvpn"
# accept the Agreement to start the OpenVPN Access Server 

# add non-privileged user 
# add the user "HanetakaYuminaga" from the https://localhost:8080/admin "USER MANAGEMENT"
/usr/local/openvpn_as/scripts/sacli --user HanetakaYuminaga --new_pass 'your-cool-password' SetLocalPassword ## set the password by the commandline
/usr/local/openvpn_as/scripts/sacli start
systemctl restart openvpnas

# config firewall
firewall-cmd --add-service openvpn ## --zone=public
# firewall-cmd --info-service=openvpn ## --zone=public
# firewall-cmd --list-services ## --zone=public
firewall-cmd --add-masquerade ## --zone=public
# firewall-cmd --query-masquerade ## --zone=public
firewall-cmd --runtime-to-permanent
firewall-cmd --reload

# systemctl stop sshd ## stop sshd for security ## we leave the sshd enabled and we may restart the machine by the Vultr to start the sshd automatically
```

#### 2\.import OpenVPN profile

##### common
```shell
ssh -L8080:localhost:943 root@x.x.x.x ## use ssh forwarding to tunnel through the firewall
# access the https://localhost:8080 (without the "/admin") by your web browser
# your web browser may warn the website is unsafe and we may ignore the warning
# login with the non-privileged user "HanetakaYuminaga"
# download the profile file "client.ovpn" from the link "Yourself (user-locked profile)"
```

##### Windows/Mac/Android/IOS client
```shell
# download the client from the https://localhost:8080 (without the "/admin") by your web browser 

# install the client and import the profile from the file "client.ovpn" by the client UI
```

##### Linux client  
```shell
# we don't need to download the client and we may use the "plasma-nm-openvpn"
nmcli connection import type openvpn file "path-to-the-client.ovpn" ## import the profile
# "configure" the "Connections" and fill the "username" with "openvpn" by the plasma-nm UI ## leave the "Private Key Password" blank
```  

#### 3\.connect OpenVPN

##### Windows/Mac/Android/IOS client  
```shell
# connect to the imported profile by the client UI
```

##### Linux client  
```shell
# connect by the plasma-nm UI ##  leave the "(Private) key Password" blank
```

### III\.Tor

You may rent the CentOS 8 machine by the Vultr and deploy your own Tor server by the following tutorial.

#### 1\.server side  

install Tor  
```shell
# no obfs4 repo available
yum install https://kojipkgs.fedoraproject.org/packages/obfs4/0.0.11/2.fc32/x86_64/obfs4-0.0.11-2.fc32.x86_64.rpm #yum install obfs4 #used by BridgeRelay

echo '[tor]
name=Tor for Enterprise Linux $releasever - $basearch
baseurl=https://rpm.torproject.org/centos/$releasever/$basearch
enabled=1
gpgcheck=1
gpgkey=https://rpm.torproject.org/centos/public_gpg.key
cost=100' > /etc/yum.repos.d/tor.repo

yum install tor
```

edit Tor config
```shell
vi /etc/tor/torrc

- #SOCKSPort 9050 # Default: Bind to localhost:9050 for local connections.
+ SOCKSPort 0 # Set "SOCKSPort 0" if you plan to run Tor only as a relay, and not make any local application connections yourself.

- #RunAsDaemon 1
+ RunAsDaemon 1

- #ORPort 9001
+ ORPort 9001

- #Nickname ididnteditheconfig
+ Nickname TorofHanetakaYuminaga #your cool nickname

- #ExitRelay 1
+ ExitRelay 0

- #BridgeRelay 1
+ BridgeRelay 1

```

start Tor service
```shell
firewall-cmd --add-port 9001/tcp ## --zone=public ## configure firewalld to allow the "ORPort"
# firewall-cmd --list-ports ## --zone=public
firewall-cmd --add-masquerade ## --zone=public
# firewall-cmd --query-masquerade ## --zone=public
firewall-cmd --runtime-to-permanent
firewall-cmd --reload

systemctl enable tor
systemctl restart tor
#systemctl status tor
```

#### 2\.client side  

##### Windows/MacOS/Linux client

download the "Tor Browser" from https://www.torproject.org/download/

open the "Tor Browser" and config the bridge "x.x.x.x:9001" by the UI  
the "Tor Browser" will launch the "Tor" and listen on localhost:9150 #you can use "ps" to find the related command args of "Tor"  

launch app with socks5 proxy (suggested)
```shell
#close all opened "chrome"s 

"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --proxy-server="socks5://localhost:9150" #Windows

"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --proxy-server="socks5://localhost:9150" & #MacOS

google-chrome --proxy-server="socks5://localhost:9150" & #Linux
```

other usage (not suggested) / set the socks5 proxy in system settings
```shell
KDE5/System Settings/Network/Settings/Proxy/Use system proxy configuration:/SOCKS Proxy:socks5://localhost:9050
#https://wiki.archlinux.org/index.php/Proxy_server#Proxy_settings_on_GNOME3
```

##### Linux client (Tor without the Tor Browser)

install Tor packages
```shell
echo '[tor]
name=Tor for Enterprise Linux $releasever - $basearch
baseurl=https://rpm.torproject.org/centos/$releasever/$basearch
enabled=1
gpgcheck=1
gpgkey=https://rpm.torproject.org/centos/public_gpg.key
cost=100' > /etc/yum.repos.d/tor.repo

yum install tor
```

edit Tor config
```
vi /etc/tor/torrc

+ UseBridges 1

+ Bridge x.x.x.x:9001

- SOCKSPort 9050 # Default: Bind to localhost:9050 for local connections.
+ SOCKSPort 9050 # Default: Bind to localhost:9050 for local connections.

- #RunAsDaemon 1
+ RunAsDaemon 1
```

start Tor service
```shell
systemctl enable tor
systemctl restart tor
#systemctl status tor
```

launch app with socks5 proxy (suggested)
```shell
#close all opened "google-chrome"s 
google-chrome --proxy-server="socks5://localhost:9050" &
#systemctl restart tor #we may restart tor from time to time if the network is too slow
```

other usage (not suggested) / set the socks5 proxy in system settings
```shell
KDE5/System Settings/Network/Settings/Proxy/Use system proxy configuration:/SOCKS Proxy:socks5://localhost:9050
#https://wiki.archlinux.org/index.php/Proxy_server#Proxy_settings_on_GNOME3
```

##### Android dlient
https://github.com/guardianproject/orbot/releases
