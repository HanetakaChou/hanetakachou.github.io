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

#### server  
```shell  
# ssh root@x.x.x.x

yum install https://as-repository.openvpn.net/as-repo-centos8.rpm
yum install openvpn-as

# /usr/local/openvpn_as/bin/ovpn-init
# systemctl status openvpnas

passwd openvpn
systemctl stop firewalld
```

#### client  
```shell
# https://x.x.x.x:943
# https://x.x.x.x:943/admin

# openvpn client
# import profile from URL https://x.x.x.x:943
```

#### server  
```shell
# ssh root@x.x.x.x

systemctl start firewalld

firewall-cmd --add-service openvpn ##--zone=public 
firewall-cmd --add-masquerade
# firewall-cmd --query-masquerade
firewall-cmd --runtime-to-permanent
firewall-cmd --reload
```

#### client  
```shell
# openvpn client
# connect to profile
```