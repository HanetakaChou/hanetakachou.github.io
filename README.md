## License  
```  
Copyright (C) YuqiaoZhang

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License along with this program.  If not, see <https://www.gnu.org/licenses/>
```  
   
   
[Logic.md](Logic.md)  

## Analysis  
   
> [Analysis/1_Real_Analysis.md](Analysis/1_Real_Analysis.md)    

## Algebra  

> [Algebra/1_Linear_Algebra.md](Algebra/1_Linear_Algebra.md)   

## Computer  

[Compiler.md](Compiler.md)  

## Scientific Web Browsing

### I\. SSH
You may rent the CentOS 8 machine by the Vultr and use ssh as a socks5 proxy server.

#### 1\.server side  

set firewall rules
```shell
# systemctl start sshd # by default

# firewall-cmd --add-service ssh ## by default
# firewall-cmd --list-services ## --zone=public
firewall-cmd --add-masquerade ## --zone=public
# firewall-cmd --query-masquerade ## --zone=public
firewall-cmd --runtime-to-permanent
firewall-cmd --reload
```
create non-privileged user
```shell
adduser -m HanetakaYuminaga
passwd HanetakaYuminaga
```

disable root login from ssh for security
```shell
vi /etc/ssh/sshd_config  
- PermitRootLogin yes
+ PermitRootLogin no

rm /usr/bin/su #learn from Android
```

#### 2\.client side

use ssh as a socks5 proxy server
```shell
ssh -T -D 8080 HanetakaYuminaga@x.x.x.x #add "-T" to disable pseudo-tty allocation for better performance
```

launch app with http proxy  
```shell
#launch from the local terminal not the ssh terminal

#close all opened "chrome"s 

"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --proxy-server="socks5://localhost:8080" #Windows

"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --proxy-server="socks5://localhost:8080" & #MacOS

google-chrome --proxy-server="socks5://localhost:8080" & #Linux
```

### II\. Privoxy

You may rent the CentOS 8 machine by the Vultr and deploy your own (http) proxy server by the following tutorial.

#### 1\.server side  

install Privoxy
```shell
yum install privoxy

# firewall-cmd --add-service privoxy ## --zone=public #**NOT DO THIS**, which may allow anyone to connect to the privoxy
# firewall-cmd --list-services ## --zone=public
firewall-cmd --add-masquerade ## --zone=public
# firewall-cmd --query-masquerade ## --zone=public
firewall-cmd --runtime-to-permanent
firewall-cmd --reload
```

create non-privileged user
```shell
adduser -m HanetakaYuminaga
passwd HanetakaYuminaga
```

disable root login from ssh for security
```shell
vi /etc/ssh/sshd_config  
- PermitRootLogin yes
+ PermitRootLogin no

rm /usr/bin/su #learn from Android
```

#### 2\.client side

use ssh forward to encrypt the privoxy   
```shell
#the default listen address of Privoxy is "127.0.0.1:8118" 
#/etc/privoxy/config 
#listen-address 127.0.0.1:8118

ssh -T -L8118:localhost:8118 HanetakaYuminaga@x.x.x.x #add "-T" to disable pseudo-tty allocation for better performance
#for vscode, add the "LocalForward 127.0.0.1:8118 127.0.0.1:8118" in ssh config file #https://code.visualstudio.com/docs/remote/ssh#_always-forwarding-a-port
```

launch app with http proxy  
```shell
#launch from the local terminal not the ssh terminal

#close all opened "chrome"s 

"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --proxy-server="localhost:8118" #Windows

"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --proxy-server="localhost:8118" & #MacOS

google-chrome --proxy-server="localhost:8118" & #Linux
```

### III\.OpenVPN Access Server

You may rent the CentOS 8 machine by the Vultr and deploy your own VPN server by the following tutorial.

#### 1\.install OpenVPN Access Server

##### server side  
```shell  
yum install https://as-repository.openvpn.net/as-repo-centos8.rpm
yum install openvpn-as

# /usr/local/openvpn_as/bin/ovpn-init ## we may generate another new profile and leave the old one invalid from time to time for security
passwd openvpn ## set the password of the user "openvpn"
```

#### 2\.import OpenVPN profile

##### server side  
```shell  
firewall-cmd --add-port 943/tcp ## --zone=public ## configure firewalld to allow the https access to import the profile
# firewall-cmd --list-ports ## --zone=public
firewall-cmd --add-masquerade ## --zone=public
# firewall-cmd --query-masquerade ## --zone=public
firewall-cmd --runtime-to-permanent
firewall-cmd --reload
```

##### client side  

###### common
```shell
# access the https://x.x.x.x:943/admin (with the "/admin") by the web browser and accept the Agreement to start the OpenVPN Access Server ## login with the user "openvpn" 
# the web browser may warn the website is unsafe and we may ignore the warning
```

###### Windows/Mac/Android/IOS client
```shell
# download the client from the URL https://x.x.x.x:943 (without the "/admin") by the web browser ## login with the user "openvpn" ## the web browser may warn the website is unsafe and we may ignore the warning
# install the client and import the profile from the URL https://x.x.x.x:943 (without the "/admin") by the client UI
```

###### Linux client  
```shell
# we don't need to download the client and we may use the "plasma-nm-openvpn"

# download the profile file "client.ovpn" from the URL https://x.x.x.x:943 (without the "/admin")
nmcli connection import type openvpn file path-to-client.ovpn ## import the profile

# "configure" the "Connections" and fill the "username" with "openvpn" by the plasma-nm UI
```  

##### server side  
```shell  
# ssh root@x.x.x.x

firewall-cmd --remove-port 943/tcp ## start firewalld for security and we can't access the "unsafe" URL https://x.x.x.x:943 now
firewall-cmd --runtime-to-permanent
firewall-cmd --reload
```

#### 3\.connect OpenVPN

##### server side  
```shell  
# ssh root@x.x.x.x

firewall-cmd --add-service openvpn ## --zone=public
# firewall-cmd --list-services ## --zone=public
firewall-cmd --add-masquerade ## --zone=public
# firewall-cmd --query-masquerade ## --zone=public
firewall-cmd --runtime-to-permanent
firewall-cmd --reload

systemctl restart openvpnas ## to start/stop the firewalld may result in that the VPS doesn't work
# systemctl status openvpnas

# systemctl stop sshd ## stop sshd for security ## we leave the sshd enabled and we may restart the machine by the Vultr to start the sshd automatically
```

##### client side  
```shell
# openvpn client
# connect to the imported profile
```

###### Windows/Mac/Android/IOS client  
```shell
# connect to the imported profile by the client UI
```

###### Linux client  
```shell
# connect by the plasma-nm UI ##  leave the "key Password" empty
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
