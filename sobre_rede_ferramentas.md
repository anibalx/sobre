# FERRAMENTAS

## Telnet
Testa a conexão a um IP, por uma porta específica
```
  telnet <IP> <PORT>
```
> ao passar um número de uma porta que não existe, SERVER envia um RST (Reset == "não entendi")

## NetCat (NC)
Testa a conexão a um IP (TCP, UDP etc.), por uma porta específica
```
  nc -vz <IP> <PORT>
  netcat -vz <IP> <PORT>
```

Abre uma porta local
* -l == lista a porta
* -k == não mata a porta depois da conexão
```
  nc -l -k <PORT>
  netcat -l -k <PORT>
```

Abre uma conexão para receber e uma conexão para enviar um arquivo
* -l == lista a porta
* -N == abra e feche a conexão após o fim da transferência do arquivo
```
  nc -l <PORT> > <FILE_NAME> # porta do servidor e arquivo a ser recebido
  nc -N <IP> <PORT> < <FILE_NAME> # ip do servidor porta do servidor e arquivo a ser enviado

  nc -l 1234 > file_name.receive
  nc -N 127.0.0.1 1234 file_name.send
```

Compacta num lado e descompacta numa porta
```
  nc -l -k <PORT> | tar xvzf - 
  tar cvzf <DIR_FROM_TEST> | nc <IP> <PORT>
```

Cria uma conexão e fica esperando alguém conectar
* --vv == exibe toda a saída
* -n   == ignora nome (DNS)
* -p   == porta
* -k   == fechou uma conexão, abra outra (mantenha a conexão)
```
  nc -l -vv -n -p -k <PORT>
```

## NMAP
Testa a conexão a um IP, por uma porta específica
* -PN = trata dos hosts já conectados, sem a necessidade de descobrir sua presença em rede
```
  nmap -Pn -p <PORT> <IP>
```

* -sT = scan em portas TCP
* -sU = scan em portas UDP
```
  nmap -sT <IP> # TCP 
  nmap -sU <IP> # UDP
```
* -T4 = IPv4
```
  nmap -T4 192.168.0.0/24
```


## TCPDUMP
Captura do fluxo de rede
* -n        = não resolve nome
```
  sudo tcpdump -n
```

Captura frame Ethernet
* -e          = exibe link-level, camada 2 (Ethernet e IEEE 802.11)
```
  sudo tcpdump -e
```

Captura um pacote IP (TCP, UDP etc.) e exibe em hexadecimal
* -n 				= não resolve nome
* ip 				= ipv4
* -c <NUM> 	= pacotes
* -x 				= hexadecimal
```
  sudo tcpdump -n ip -c 1 -x 
```

Captura dois pacotes IP (segmento ICMP) e exibe o MAC Address
* -n 				= não resolve nome
* icmp 			= icmp
* -c <NUM> 	= pacotes
* -e 				= exibe MAC Address
```
  sudo tcpdump -n icmp -c 2 -e
```

Captura dois pacotes IP, numa interface (placa) de rede e mostra o MAC Address
* -n 				= não resolve nome
* -i eth0   = use uma interface de rede
* -c <NUM> 	= pacotes
* -e 				= exibe MAC Address
```
  sudo tcpdump -ni eth0 -c 2 -e
```

Exibe o payload (-A) do que trafega na rede (-i)
* -i        = use uma interface de rede
* -A        = exibe o payload
```
  sudo tcpdump -i -A
```

Realiza um sniffer (escutador de rede) em um host específico.
* -n 				= não resolve nome
* host      = IP a ser capturado
```
  sudo tcpdump -n host <IP>
```

Realiza um sniffer (escutador de rede) na rede local.
* -i        = use uma interface de rede
* -A        = exibe o payload
* -nnn      = não resolva nome e limpe a exibição
* any       = qualquer
* port      = as portas que devem estar a escuta
* host      = IP a ser capturado
```
  sudo tcpdump -i any port <PORT> and host <IP>
  sudo tcpdump -i any port <PORT> and host <IP> -A    # veja o que trafega pela rede
  sudo tcpdump -nnn -i any port <PORT> and host <IP>  # limpa a exibição
```

Exibe data e hora completos
* -tttt     = ano, mês, dias, hora, minuto, segundos e frações de segundos
```
  sudo tcpdump -tttt
```

Gera arquivo
* -n             = não resolva nome
* -i             = use uma interface de rede
* lo             = use interface loopback
* -v             = mostra informações sobre o IP
* -w <FILE>.pcap = grava saída em um arquivo
* any            = qualquer
* host           = IP capturado
```
  sudo tcpdump -ni lo -v -w <FILE>.pcap
  sudo tcpdump -i -w <FILE>.pcap
  sudo tcpdump -i any port <PORT> and host <IP> -w <FILE>.pcap   
```

> Leia o arquivo
**OBS**: -n -r, o -r permite reconhecer o arquivo.pcap, possilitando usar o autocompletar
```
  sudo tcpdump -n -r <FILE>.pcap
  sudo tcpdump -nr <FILE>.pcap
  sudo tcpdump -nr <FILE>.pcap -A  # -A == exibição em ASCII: cabeçalho e payload
```
  :\s  | dois-pontos e espaço | separa protocolos
   .   | pontinho signica ACK | está em todas as linhas, menos a primeira
length | tamanho do payload   | Apenas o PUSH possui payload e tcpdump prioriza o TCP
   E.  | início cabeçalho IP  | ASCII(E) == 45 -> 4 == version | 5 IHL ; ASCII(.) == 00

**OBS**
> No caso de um download muito grande, o P (de Push) pode ser omitido
  e um ponto (.) similar ao ACK, colocado na exibição do tcpdump


## TSHARK
Wireshark em linha de comando
> Leia o arquivo
```
  tshark -n -r <FILE>.pcap
```

## LSPCI
**Barramento PCI** uma placa de rede, por exemplo

* mostra as caracteristicas do módulo/driver (dispositivo) 
do tipo ethernet, onde são usados cabos de rede
* -nn = mostra os nomes e números do ID dos dispositivos
* -k  = drivers do kernel
* -d  = mostra os dispositivos específicos
```
  lspci -nnkd::0200
```

* mostra as caracteristicas do módulo/driver (dispositivo) WiFi
* -nn = mostra os nomes e números do ID dos dispositivos
* -k  = drivers do kernel
* -d  = mostra os dispositivos específicos
```
  lspci -nnkd::0280
```

## LSUSB
**Barramento USB** uma placa de rede, por exemplo

* mostra as caracteristicas do módulo/driver (dispositivo) 
do tipo ethernet, onde são usados cabos de rede
* -t = mostra a árvore de hierarquia dos dispositivos usb físicos
* -v = verbose
```
  lsusb -tv
```

## LSOF
Lista os arquivos abertos
* -i  = lista os arquivos especificamente sobre endereço de internet
* -i4 = mesmo que i, mas para ipv4
* -i6 = mesmo que i, mas para ipv6
* tcp = mostra referente ao protocolo tcp
* udp = mostra referente ao protocolo udp
* :<PORT> = mostra referente a um serviço
* -t  = exibe apenas o PID
```
  lsof -i
  lsof -i4
  lsof -i6
  lsof -i tcp
  lsof -i udp
  lsof -i:<PORT> 
  lsof -t -i:<PORT> 
```

## PACKIT
O padrão é TCP
* -d == rede e host a ser enviado
* -F == Flags: (S)YN, (P)USH, (R)ESET
```
  packit -d 10.0.0.5 -F SPR
```

## IP
* mostra todos os dispositivos hiabilitados e
* se estão up (ligado) ou down (desligado)
```
  ip link
  ip l
  ip link set <REDE> up   # Suba a rede
  ip link set <REDE> down # Baixe a rede
```


* qual o IP atribuio as interfaces de redes disponíveis  
* qual o MAC address  
* nome de cada interface  
* tamanho do pacote  
```
  ip address
  ip a
```

* enviaum ARP dentro da rede e exibe IP com MAC Address
```
  ip n # arp -an
```

* mostra as rotas que os pacotes terão de tomar, pelo gateway  
```
  ip route
  ip r
```

* default via <IP> = para que máquina dentro da rede os pacotes serão enviados  
* <IP>/CIDR = rede na qual esta máquina esta inserida  
* src <IP>  = própria máquina (ou servidor DHCP)
```
  default via 192.168.86.97 dev enp2s0 proto dhcp metric 20100 
  192.168.86.0/24 dev enp2s0 proto kernel scope link src 192.168.86.2 metric 100
```

## ss
Lista os sockets abertos no sistema
* -o = options
```
  ss -o state established '( sport = :http or sport = :https )'
```
* -t  = mostra para TCP
* -n  = não resolva o DNS
* src = seta a porta de origem, pode ser 80 ou 443
```
  ss -tn src :80 or src :443
```

## Fuser
Identifique processos usando arquivos ou sockets
```
  fuser 443/tcp
  fuser 68/udp
```

## ipcalc
```
  ipcalc
```

## Traceroute
Manda um pacote com ttl=1
1º roteador devolve: icmp=0 (tipo 11, código 0: expirado) + IP
Manda um pacote com ttl=2
1º roteador devolve: icmp=1 + IP
2º roteador devolve: icmp=0 (tipo 11, código 0: expirado) + IP
Manda um pacote com ttl=3
1º roteador devolve: icmp=2 + IP
2º roteador devolve: icmp=1 + IP
3º roteador devolve: icmp=0 (tipo 11, código 0: expirado) + IP
* -n = ignore resolução de nomes
* -I = mande uma pacote ICMP
```
  traceroute -nI <IP>
```

* -p = excolha a porta
```
  traceroute -p <PORT> <IP>
```

## Tracepath
Traça caminho para um host de rede 
descobrindo MTU ao longo deste caminho
```
  tracepath google.com
```

* -4      = use apenas IPv4
```
  tracepath -4 <IP>
```

* -6      = use apenas IPv6
```
  tracepath -6 <IP>
```

* -6      = use apenas IPv6
```
  tracepath -6 3ffe:2400:0:109::2
```

* -n      = imprima, principalmente, endereços IP numericamente
```
  tracepath -n <IP>
```


## MTR
Manda um pacote com ttl=1
1º roteador devolve: icmp=0 (tipo 11, código 0: expirado) + IP
Manda um pacote com ttl=2
1º roteador devolve: icmp=1 + IP
2º roteador devolve: icmp=0 (tipo 11, código 0: expirado) + IP
Manda um pacote com ttl=3
1º roteador devolve: icmp=2 + IP
2º roteador devolve: icmp=1 + IP
3º roteador devolve: icmp=0 (tipo 11, código 0: expirado) + IP
* -n = ignore resolução de nomes
```
  mtr -n <IP>
```
---

# Conectividade
Quando uma máquina consegue enviar um pacote de rede e receber resposta

## PING
Cria um pacote ICMP request e espera um ICMP response
* rtt      = round trip time (tempo de viagem de ida e volta)
* icmp_seq = sequẽncia de pacotes ICMP enviados  
* ttl      = caracaterística do tempo de vida dos pacotes TCP, 
             produzido pelo OS (Windows 128, Linux 64, Unix 255)
             seu local em Linux: /proc/sys/net/ipv4/ip_default_ttl
             em geral, o valor do ttl corresponde ao tipo de OS
             imediatamente acima: 
             49 == Linux (64 - 49 = 15 roteadores), 
             108 == Windows (128 - 110 = 28 roteadores)
             e colocado dentro do pacote IP 
             onde cada roteador pelo qual passa, perde 1
             se chegar a zero, o roteador (que fez de 1 a 0)
             deve avisar a origem que o ttl expirou
* time     = tempo decorrido para o pacote ir e voltar  
```
  ping -c 3 1.1.1.1
```


## ARPING
Realiza uma requisição (request) ARP a um host vizinho
```
  arping <IP>
```

## NETDISCOVER
Pega tudo que passa em rede e monta uma tabela ARP-MAC
```
  netdiscover
```

---

# Firmware
Rodo no processador do pŕoprio dispositivo 
(não no processador principal da máquina - onde roda o kernel)
## MODINFO
Permite averiguar as informações sobre o módulo que roda 
no processador do dispositivo disponibilizado pelo provedor
```
  modinfo firm.fw
```

---

# Core
Simulador e emulador de redes
## Instalação
> docker e tigervnc
```
  install docker.io tigervnc-viewer
```
## Execute o Docker
```
  docker run -d --cap-add=NET_ADMIN --cap-add=SYS_ADMIN -p 5900:5900 -p 8080:8080 d3f0/coreemu_vnc
```
## Execute o tigerVNC
```
  tigervnc
```
> aponte para o IP no qual roda o docker e clique em conectar
```
  127.0.0.1
```
> coloque a senha
```
  coreemu
```

---

# IPTABLES
* -L || -list == lista todas as regras
```
  iptables -L
```

IPTABLES, bloqueie tudo que vier para a porta 81 desta máquina
* -A || --append   INPUT == esta máquina
* -p || --protocol tcp   == protocolo
* --dport                == porta
* -j || --jump     DROP  == descarte
```
  iptables -A INPUT -p tcp --dport 81 -j DROP
```

---

## HOST
Demonstra DNS e IP
* -4  = retorna IPv4
```
  host -4 myip.opendns.com resolver1.opendns.com
  curl ifconfig.me
```
