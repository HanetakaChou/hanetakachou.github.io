## License  
```  
Copyright (C) YuqiaoZhang

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License along with this program.  If not, see <https://www.gnu.org/licenses/>
```  
   
   
[Logic.md](Logic.md)  

### Analysis  
   
> [Analysis/_1_Topology_Metric.md](Analysis/_1_Topology_Metric.md)   
> [Analysis/_2_Measure.md](Analysis/_2_Measure.md)    
> [Analysis/_3_Calculus.md](Analysis/_3_Calculus.md)    

[Calculus.md](Calculus.md)    

[Complex.md](Complex.md)  

[LinearAlgebra.md](LinearAlgebra.md)   

[Compiler.md](Compiler.md)  

### VPS

You may rent the CentOS 8 server by the Vultr and deploy your own VPS by the following tutorial.

#### 1\.Install VPS

##### Server-Side  
```shell  
# ssh root@x.x.x.x

yum install https://as-repository.openvpn.net/as-repo-centos8.rpm
yum install openvpn-as

# /usr/local/openvpn_as/bin/ovpn-init ## we may generate another new profile and leave the old one invalid from time to time for security
passwd openvpn ## set the password of the user "openvpn"
```

#### 2\.Import Profile

##### Server-Side  
```shell  
# ssh root@x.x.x.x

firewall-cmd --add-port 943/tcp ## --zone=public ## configure firewalld to allow the https access to import the profile
# firewall-cmd --list-ports ## --zone=public
firewall-cmd --add-masquerade ## --zone=public
# firewall-cmd --query-masquerade ## --zone=public
firewall-cmd --runtime-to-permanent
firewall-cmd --reload
```

##### Client-Side  

###### Common
```shell
# access the https://x.x.x.x:943/admin (with the "/admin") by the web browser and accept the Agreement to start the OpenVPN Access Server ## login with the user "openvpn" 
# the web browser may warn the website is unsafe and we may ignore the warning
```

###### Windows/Mac/Android/IOS Client
```shell
# download the client from the URL https://x.x.x.x:943 (without the "/admin") by the web browser ## login with the user "openvpn" ## the web browser may warn the website is unsafe and we may ignore the warning
# install the client and import the profile from the URL https://x.x.x.x:943 (without the "/admin") by the client UI
```

###### Linux Client  
```shell
# we don't need to download the client and we may use the "plasma-nm-openvpn"

# download the profile file "client.ovpn" from the URL https://x.x.x.x:943 (without the "/admin")
nmcli connection import type openvpn file path-to-client.ovpn ## import the profile

# "configure" the "Connections" and fill the "username" with "openvpn" by the plasma-nm UI
```  

##### Server-Side  
```shell  
# ssh root@x.x.x.x

firewall-cmd --remove-port 943/tcp ## start firewalld for security and we can't access the "unsafe" URL https://x.x.x.x:943 now
firewall-cmd --runtime-to-permanent
firewall-cmd --reload
```

#### 3\.Connect

##### Server-Side  
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

##### Client-Side  
```shell
# openvpn client
# connect to the imported profile
```

###### Windows/Mac/Android/IOS Client  
```shell
# connect to the imported profile by the client UI
```

###### Linux Client  
```shell
# connect by the plasma-nm UI ##  leave the "key Password" empty
```

### Tor

You may rent the CentOS 8 server by the Vultr and deploy your own Tor (Bridge)Relay by the following tutorial.

#### Server-Side  

install Tor package
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
+ Nickname yourcoolnickname

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

#### Client-Side  

##### Linux Client

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

other usage (not suggested) / torsocks works only for limited client
```shell
torsocks curl https://api.ipify.org?format=json
#torsocks google-chrome #unsupported
```

##### Windows Client

install Tor packages
download the "Windows Expert Bundle" from https://www.torproject.org/download/tor/

edit Tor config
```
notepad.exe C:\Users\<your_username>\AppData\Roaming\tor\torrc

+ UseBridges 1

+ Bridge x.x.x.x:9001

+ SOCKSPort 9050 # Default: Bind to localhost:9050 for local connections.
```

start Tor service
run the "tor.exe" from the downloaded "Windows Expert Bundle"  

launch app with socks5 proxy (suggested)
```shell
#close all opened "chrome"s 
"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --proxy-server="socks5://localhost:9050" #--host-resolver-rules="MAP * 0.0.0.0 , EXCLUDE localhost"
```

##### Android Client
https://github.com/guardianproject/orbot/releases