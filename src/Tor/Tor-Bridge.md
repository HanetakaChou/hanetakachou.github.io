# Tor Bridge 

You may rent the CentOS 8 machine by the Vultr / Alibaba Cloud and deploy your own Tor bridge by the following tutorial.

## 1\.deploy Tor bridge (server side)

### 1-1\.install Tor  
```bash

yum install epel-release
yum update

yum install tor

# enable automatic update 
yum install dnf-automatic
systemctl enable dnf-automatic-install.timer
systemctl restart dnf-automatic-install.timer
# systemctl status dnf-automatic-install.timer
```

### 1-2\.edit Tor config
```bash
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

### 1-3\.start Tor service
```bash
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

## 2\.use Tor bridge (client side)

### 2-1\.client side - Linux/MacOS/Windows

#### 2-1-1\.use Tor Browser  
download the "Tor Browser" from https://www.torproject.org/download/

open the "Tor Browser" and config the bridge "x.x.x.x:9001" by the UI  
the "Tor Browser" will launch the "Tor" and listen on localhost:9150 #you can use "ps" to find the related command args of "Tor"  

#### 2-1-2\.launch app with socks5 proxy (suggested)
```bash
#close all opened "chrome"s 

"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --proxy-server="socks5://localhost:9150" #Windows

"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --proxy-server="socks5://localhost:9150" & #MacOS

google-chrome --proxy-server="socks5://localhost:9150" & #Linux
```

#### 2-1-3\.other usage (not suggested) / set the socks5 proxy in system settings  
```bash
KDE5/System Settings/Network/Settings/Proxy/Use system proxy configuration:/SOCKS Proxy:socks5://localhost:9050
#https://wiki.archlinux.org/index.php/Proxy_server#Proxy_settings_on_GNOME3
```

### 2-2\.client side - Linux (Tor without the Tor Browser)

#### 2-2-1\.install Tor  
```bash

yum install epel-release
yum update

yum install tor

# enable automatic update 
yum install dnf-automatic
systemctl enable dnf-automatic-install.timer
systemctl restart dnf-automatic-install.timer
# systemctl status dnf-automatic-install.timer
```

#### 2-2-2\.edit Tor config
```bash
vi /etc/tor/torrc

+ UseBridges 1

+ Bridge x.x.x.x:9001

- SOCKSPort 9050 # Default: Bind to localhost:9050 for local connections.
+ SOCKSPort 9050 # Default: Bind to localhost:9050 for local connections.

- #RunAsDaemon 1
+ RunAsDaemon 1
```

#### 2-2-3\.start Tor service
```shell
systemctl enable tor
systemctl restart tor
#systemctl status tor
```

#### 2-2-4\.launch app with socks5 proxy (suggested)
```shell
#close all opened "google-chrome"s 
google-chrome --proxy-server="socks5://localhost:9050" &
#systemctl restart tor #we may restart tor from time to time if the network is too slow
```

#### 2-2-5\.other usage (not suggested) / set the socks5 proxy in system settings
```shell
KDE5/System Settings/Network/Settings/Proxy/Use system proxy configuration:/SOCKS Proxy:socks5://localhost:9050
#https://wiki.archlinux.org/index.php/Proxy_server#Proxy_settings_on_GNOME3
```

### 2-3\.client side -Android (orbot)
https://github.com/guardianproject/orbot/releases