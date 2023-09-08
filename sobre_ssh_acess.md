# PÓS-INSTALAÇÃO DISTRO IN VM

(de dentro da vm) pega ip da vm:
```sh
	ip -c a
```  

(de fora da vm) estabeleça conexao ssh:
```sh
	ssh <MEU_USER_IN_VM>@<IP DA VM> -p 22
```  

---

# Exemplo Akita: poking a hole
Dentro da máquina remota, adentre ao arquivo:
> em Debian
```
    vim /etc/ssh/ssh_config.d/config
```  

> em OpenSuse
```
    vim /usr/etc/ssh/ssh_config
```  


Edite as linhas
```
    #AllowTcpForwarding yes
    #GatewayPorts no

    AllowTcpForwarding yes
    GatewayPorts yes

    #Port 22
    Port 80
```  

Reeinicie o daemon e saia da máquina remota acima
```
    systemctl restart sshd && exit
```  

Logue na máquina remota através da nova porta e saia
```
    ssh root@137.184.74 -p 80
    exit
```  

Linux, conecte no meu programa de sshd,
na porta 80 do servidor da digital ocean (ip 137.184.74)
se pendure na porta 7000 de lá (ip 137.184.74:7000) e fique escutando.  
Toda vez que vier uma requisição por lá (ip 137.184.74:7000),
encaminhe (redirecione) todo tráfego para a porta 3000
da minha máquina local (ip 127.0.0.1:3000)
* -R = Especifica que as conexões com a porta TCP ou soquete Unix dada no host remoto (servidor) devem ser encaminhadas para o lado local.
* -N = Não execute um comando remoto; útil para portas encaminhadas (forwarding)
* -f = configfile
* -p = porta
```
    ssh -R <PORTA_DIGITAL_OCEAN>:<IP_MÀQUINA_LOCAL>:<PORTA_LOCAL> -N -f <MEU_USER_IN_DIGITAL_OCEAN>@<IP_MÀQUINA_DIGITAL_OCEAN> -p <PORTA_DO_SERVIDOR>
    ssh -R 7000:127.0.0.1:3000 -N -f root@137.184.74 -p 80
```  

---

# Exemplo Akita: proxy
Dentro da máquina remota, adentre ao arquivo:
```
    vim /etc/ssh/ssh_config.d/config
```  

Edite as linhas
```
    #AllowTcpForwarding yes
    #GatewayPorts no

    AllowTcpForwarding yes
    GatewayPorts yes

    #Port 22
    Port 51234
```  

Reeinicie o daemon e saia da máquina remota acima
```
    systemctl restart sshd && exit
```  

Logue na máquina remota através da nova porta
```
    ssh root@137.184.74 -p 80
```  

Linux, conecte no meu programa de sshd,
na porta 51234 do servidor da digital ocean (ip 137.184.74)  
Pendure a porta 1337 daqui (ip 127.0.0.1:1337) e fique escutando.  
Toda vez que vier uma requisição por lá (ip 137.184.74:51234),
encaminhe (redirecione) todo tráfego para a porta 1337
da minha máquina local (ip 127.0.0.1:3000)
* -D = faça bind (ligue) a máquina local
* -q = quiet mode
* -C = comprima o conteúdo que passar por este programa
* -N = não abra linha de comando com o servidor
* -p = porta
```
    ssh -D <PORTA_MAQUINA_LOCAL> -q -C -N <MEU_USER_IN_DIGITAL_OCEAN>@<IP_MÀQUINA_DIGITAL_OCEAN> -p <PORTA_DO_SERVIDOR>
    ssh -D 1337 -q -C -N root@137.184.74 -p 51234
```  

Configure o proxy
```
    127.0.0.1 1337
```  

# REFERÊNCIA
[Burlando Proxies e Firewalls ｜ Introdução a Redes Parte 5 - SSH](https://youtube.com/watch?v=T-jHuFnxZ2k)
