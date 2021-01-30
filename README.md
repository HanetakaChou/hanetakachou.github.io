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

### VPS(VPN Server)  

#### Server-Side  
```shell  
# ssh root@x.x.x.x

yum install https://as-repository.openvpn.net/as-repo-centos8.rpm
yum install openvpn-as

# /usr/local/openvpn_as/bin/ovpn-init
# systemctl status openvpnas

passwd openvpn
systemctl stop firewalld ## stop firewalld to allow the https access to import the profile
```

#### Client-Side  
```shell
# https://x.x.x.x:943
# https://x.x.x.x:943/admin

# openvpn client
# import the profile from the URL https://x.x.x.x:943
```  

##### Linux Client  
```shell
# download the profile file "client.ovpn" from the URL https://x.x.x.x:943
nmcli connection import type openvpn file path-to-client.ovpn
# fill the "username" with "openvpn" by the plasma-nm UI
```  

#### Server-Side  
```shell
# ssh root@x.x.x.x

systemctl start firewalld ## start firewalld for security

firewall-cmd --add-service openvpn ## --zone=public
# firewall-cmd --list-services ## --zone=public
firewall-cmd --add-masquerade ## --zone=public
# firewall-cmd --query-masquerade ## --zone=public
firewall-cmd --runtime-to-permanent
firewall-cmd --reload

systemctl restart openvpnas ## to start/stop the firewalld may result in that the VPS doesn't work

# systemctl stop sshd ## stop sshd for security ## we leave the sshd enabled and we may restart the machine to start the sshd automatically
```

#### Client-Side  
```shell
# openvpn client
# connect to the imported profile
```

##### Linux Client  
```shell
# connect by the plasma-nm UI ## leave the key passwd empty
```
