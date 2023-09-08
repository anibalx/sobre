ipconfig /all
ipconfig /all | findstr DNS || ipconfig /displaydns
ipconfig /displaydns | clip
ipconfig /flushdns
ipconfig /all /release "Wi-Fi"
ipconfig /all /renew


nslookup networkchuck.com
nslookup -type=mx networkchuck.com
nslookup -type=txt networkchuck.com
nslookup -type=ptr networkchuck.com

## Copia para área de transferência
clip

## Limpa tela
cls


getmac /v


powercfg /energy
powercfg /batteryreport


assoc
assoc .mp4=VLC.vlc


chkdsk /f
chkdsk /r


sfc /scannow


DISM /Online /Cleanup /Check
DISM /Online /Cleanup-Image /CheckHealth /ScanHealth


## Exibe as tarefas
tasklist | findstr script

## Mata uma tarefa
taskkill /f /pid 20184


netsh wlan show wlanreport
netsh interface ip show address | findstr "Ip Address"
netsh interface ip show dnsservers
netsh <FIREWALL> set allprofiles state off


## Ping
ping google.com
ping -t google.com

## Rota dos pacotes
tracert google.com
tracert -d google.com


netstat -af
netstat -o
netstat -e -t 5


## Exibe rotas
route print

## Adiciona rotas
route add 192.168.40.0 mask 255.255.255.0 10.7.1.44

## Deleta rotas
route delete 192.168.40.0

## Desliga máquina
shutdown /r /fw /f /t 0


# REFERÊNCIAS
# [windowns - 40 Windows Commands you NEED to know (in 10 Minutes)](http://youtube.com/watch?v=Jfvg3CS1X3A)
