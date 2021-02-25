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

## Scientific Web Browsing (by OpenVPN)

You may rent the CentOS 8 machine by the Vultr and deploy Pritunl (which is an free open source OpenVPN server) by the following tutorial.

### 1\.install Pritunl (the OpenVPN server)

```shell  
# -- server side shell -- 

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
```

```shell
# -- client side shell -- 

# https://docs.pritunl.com/docs/configuration-5  
ssh -L8080:localhost:443 root@x.x.x.x ## use ssh forwarding to tunnel through the firewall
# access the https://localhost:8080 by your web browser  
# fill the setup key with the output by the command "pritunl setup-key/*server side shell*/" and leave the MongoDB URI by default "mongodb"//localhost:27017/pritunl"

ssh -L8080:localhost:443 root@x.x.x.x ## use ssh forwarding to tunnel through the firewall
# access the https://localhost:8080 by your web browser
# fill the username with "pritunl" and password with the output by the command "pritunl default-password/*server side shell*/"
# add a server "openvpn-udp" with "4911/udp" since the port "1194/udp" (compatible with the firewalld) is denied by the SELinux  ## firewall-cmd --info-service=openvpn ## semanage port -l | grep 4911
# add a server "openvpn-tcp" with "4911/tcp" since the port "1194/tcp" is denied by the SELinux
# add an organization and add a user  
# attach the server "openvpn-udp" and "openvpn-tcp" to the organization and start the both servers
```

```shell
# -- server side shell -- 

# config firewall
firewall-cmd --permanent --new-service=pritunl
firewall-cmd --permanent --service=pritunl --add-port=4911/udp
firewall-cmd --permanent --service=pritunl --add-port=4911/tcp
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

```shell
# -- server side shell -- 

ssh -L8080:localhost:443 root@x.x.x.x ## use ssh forwarding to tunnel through the firewall
# access the https://localhost:8080 by your web browser
# fill the username with "pritunl" and password with the output by the command "pritunl default-password/*server side shell*/"
# download the user profile from the "Users" section (https://localhost:8080/#/users) 
# extract the "xxx-openvpn-udp.ovpn" and "xxx-openvpn-tcp.ovpn" from the downloaded tar file
# download the openvpn client as the following and import the profile "xxx-openvpn-udp.ovpn" and "xxx-openvpn-tcp.ovpn" by the openvpn client UI
```

##### Linux client  
```shell
# we don't need to download the openvpn client and we may use the built-in "plasma-nm-openvpn"
nmcli connection import type openvpn file "path-to-the-client.ovpn" ## import the profile by the command line
```  

##### Windows Client
```shell
# download the openvpn client from the https://openvpn.net/download-open-vpn/ by your web browser 
# https://openvpn.net/downloads/openvpn-connect-v3-windows.msi

# mirror 
# https://github.com/YuqiaoZhang/ComputerScience/releases
# https://github.com/YuqiaoZhang/ComputerScience/releases/download/openvpn-client-mirror-1.0/openvpn-connect-windows-3.2.2.1455.msi
```

##### Mac Client
```shell
# download the openvpn client from OpenVPN.Net(https://openvpn.net/download-open-vpn/)  by your web browser 
# https://openvpn.net/downloads/openvpn-connect-v3-macos.dmg

# mirror 
# https://github.com/YuqiaoZhang/ComputerScience/releases
# https://github.com/YuqiaoZhang/ComputerScience/releases/download/openvpn-client-mirror-1.0/openvpn-connect-mac-3.2.5.2468.dmg
```

##### Android Client
```shell
# download the openvpn client from F-Droid(https://github.com/schwabe/ics-openvpn) by your web browser 
# https://f-droid.org/repo/de.blinkt.openvpn_175.apk

# mirror 
# https://github.com/YuqiaoZhang/ComputerScience/releases
# https://github.com/YuqiaoZhang/ComputerScience/releases/download/openvpn-client-mirror-1.0/ics-openvpn-android-175.apk
```  

##### IOS client
```shell
# we have to download the openvpn client from AppStore(https://apps.apple.com/us/app/openvpn-connect/id590379981)
```  

#### 3\.connect OpenVPN

```shell
# connect to the imported profile by the client UI
# the "tcp" profile is more stable and recommended
```
