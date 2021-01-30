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

[Calculus.md](Calculus.md)    

[Complex.md](Complex.md)  

[LinearAlgebra.md](LinearAlgebra.md)   

[Compiler.md](Compiler.md)  

### VPS

You may rent the CentOS 8 server by the Vultr and deploy your own VPS by the following tutorial.

#### Server-Side  
```shell  
# ssh root@x.x.x.x

yum install https://as-repository.openvpn.net/as-repo-centos8.rpm
yum install openvpn-as

# /usr/local/openvpn_as/bin/ovpn-init ## we may generate another new profile and leave the old one invalid from time to time for security
passwd openvpn ## set the password of the user "openvpn"

systemctl stop firewalld ## stop firewalld to allow the https access to import the profile
```

#### Client-Side  
```shell
# access the https://x.x.x.x:943/admin by the web browser and accept the Agreement to start the OpenVPN Access Server ## login with the user "openvpn" ## the web browser may warn the website is unsafe and we may ignore the warning
```

##### Windows/ Mac / Android / IOS Client
```shell
# download the client from the URL https://x.x.x.x:943 by the web browser ## login with the user "openvpn" ## the web browser may warn the website is unsafe and we may ignore the warning
# install the client and import the profile from the URL https://x.x.x.x:943 by the client UI
```

##### Linux Client  
```shell
# we don't need to download the client and we may use the "plasma-nm-openvpn"

# download the profile file "client.ovpn" from the URL https://x.x.x.x:943
nmcli connection import type openvpn file path-to-client.ovpn ## import the profile

# "configure" the "Connections" and fill the "username" with "openvpn" by the plasma-nm UI
```  

#### Server-Side  
```shell
# ssh root@x.x.x.x

systemctl start firewalld ## start firewalld for security and we can't access the "unsafe" URL https://x.x.x.x:943 now

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

#### Client-Side  
```shell
# openvpn client
# connect to the imported profile
```

##### Windows/ Mac / Android / IOS Client  
```shell
# connect to the imported profile by the client UI
```

##### Linux Client  
```shell
# connect by the plasma-nm UI ##  leave the "key Password" empty
```
