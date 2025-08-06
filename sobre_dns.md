# NetworkManager

> /etc/resolv.conf -> DNS:208.67.222.222 ^ 208.67.222.222  

> nmcli - command-line tool for controlling NetworkManager  

## Restart NetworkManager
```
service NetworkManager restart
```  

---

## Up Down
```
nmcli con down <connectionName>
nmcli con up <connectionName>
```  

---

## Ignore and Set IPv4
```
nmcli con mod "$connectionName" ipv4.ignore-auto-dns yes
```  

```
nmcli con mod "$connectionName" ipv4.dns "8.8.8.8 8.8.4.4"
```  

```
nmcli con mod "$connectionName" ipv4.dns "208.67.222.222 208.67.222.222"
```  

---

## Shell From nmcli
```
nmcli -g name,type connection  show  --active | awk -F: '/ethernet|wireless/ { print $1 }' | while read connection
do
  nmcli con mod "$connection" ipv6.ignore-auto-dns yes
  nmcli con mod "$connection" ipv4.ignore-auto-dns yes
  nmcli con mod "$connection" ipv4.dns "8.8.8.8 8.8.4.4"
  nmcli con mod "$connectionName" ipv4.dns "208.67.222.222 208.67.222.222"
  nmcli con down "$connection" && nmcli con up "$connection"
done
```  
