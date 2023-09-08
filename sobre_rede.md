# RFC
768             | UDP
791             | IP
792             | ICMP
793             | TCP
1122            | Requirements for Internet Hosts
2131 -> 3315    | DHCP
4340            | DCCP
6890            | IPv4
8200            | IPv6
C5737           | IPv4 Address Blocks Reserved for Documentation 

# Portas
```
  /etc/services
  /usr/etc/services
```

# Protocolos de Rede
Protocolos de rede são algoritmos, capazes de realizar operações
matemáticas
Só exitem protocolos DE REDE em 4 camadas:
7. Aplicação
4. Transporte
3. Rede
2. Enlace

---

# Cabos

## Cabos de cores (lados) iguais
Cabo lados iguais, colocado em equipamentos considerados diferentes.

## Cross-Over
Cabo cruzado, colocado em equipamentos considerados iguais.
 
**OBS**
> Roteador também é considerado um computador

## MDI/MDX 
Equipamento entende o tipo de cabo conectado

## RS 232
Cabo para conexão serial (cabo azul)

---

# Rede
O OS (Operating System), sistema operacional
trabalha com intervalos de IPs
para realizar a verificação da necessidade de roteamento
para chegar a um IP

## Intervalos de IP
Os intervalos de IP, são representados por:
- Endereço de Rede      | Limite Inferior
- Endereço de Broadcast | Limite Superior

## Exemplo de como o OS trabalha
Se a máquina com a qual se deseja comunicar, pertence ao mesmo segmento de rede
Então, a máquina comunicante envia um ARP perguntando qual o MAC Address da máquina que se deseja comunicar
Além de mandar diretamente para a máquina que se deseja comunicar, o frame (quadro) Ethernet


Se a máquina com a qual se deseja comunicar, NÂO pertence ao mesmo segmento de rede
Então, a máquina comunicante envia um ARP perguntando qual o MAC Address do gateway (roteador)
Além de mandar diretamente para a máquina que se deseja comunicar, o frame (quadro) Ethernet
E o o gateway (rotador) direciona isso para o lugar a ser entregue/recebido.

## Segmento de Rede
É um endereçamento próprio, advindo de um roteador

## Representação de segmentos de redes
* segmento de rede: **10.0.0.0/8**
* broadcast:        **10.255.255.255**
* gateway:          **10.0.0.5**

* segmento de rede: **11.0.0.0/8**
* broadcast:        **11.255.255.255**
* gateway:          **11.0.0.5**
```
  Rede    10.0.0.0/8                                   Rede    11.0.0.0/8
Broadcast 10.255.255.255/8                           Broadcast 11.255.255.255/8

     ___                                                     ___
    /   |                                                   |   \  
   /    |                                                  /|    \
  /     | \     _____         Roteador          _____     / |     \
 |______|  \   |     |         ______          |     |   /  |______|
 10.0.0.1   \__|     |________|      |_________|     |__/   11.0.0.1
            /  |     |        |______|         |     |  \
    ____   /   |_____|                         |_____|   \   ____ 
   /    | /    Switch           /  \           Switch     \ |    \
  /     |/                     /    \                      \|     \
 /      |                     /      \                      |      \
|_______|                    /        \                     |_______|
 10.0.0.2                   /          \                    11.0.0.2
                       10.0.0.5     11.0.0.5
                          IP           IP
                         Placa        Placa
                          de           de
                         Rede         Rede
                      "Gateway"     "Gateway"
```

## Comunicação entre segmentos de rede
> Observe a imagem acima, e acompanhe a comunicação

### Exemplo de comunicação dentro de um mesmo segmento de rede
Humano diz: 
- IP: **10.0.0.1/8**

Computador entende:
- IP: **10.0.0.1**
- Endereço de Rede: **10.0.0.0**
- Endereço de Broadcast: **10.255.255.255**

IP:
  - é maior que o endereço de rede? SIM
  - é menor que o endereço de broadcast? SIM

Então, IP faz parte do **Segmento de Rede** e não necessita de
roteamento para chegar até lá.


### Exemplo de comunicação dentre segmentos de rede diferentes
IP **10.0.0.1** deseja comunicar com **10.0.0.2**

**PERGUNTA**
- IP **10.0.0.2** pertence ao mesmo segmento de rede que eu (**10.0.0.1**)?

**RESPOSTA**
- SIM, pois **10.0.0.2** está no intervalo entre:
1. segmento de rede: **10.0.0.0**
2. Broadcast:        **10.255.255.255**


Como já houve a identificação de partilha do mesmo segmento de rede
entre **10.0.0.1** e **10.0.0.2**, não há necessidade de roteamento

Agora, **10.0.0.1** envia um **ARP REQUEST** perguntando:
  - quem é **10.0.0.2**?

**10.0.0.2** responde
  - sou eu e **MAC Address** é tal

**10.0.0.1** responde
  - meu **MAC Address** é tal 
  - tome este Ethernet( IP(TCP) )


### Exemplo de comunicação entre de segmentos de rede diferentes
IP **10.0.0.1** deseja comunicar com **11.0.0.1**

**PERGUNTA**
- IP **11.0.0.1** pertence ao mesmo segmento de rede que eu (**10.0.0.1**)?

**RESPOSTA**
- NÃO, pois **11.0.0.1** não está no intervalo entre:
1. segmento de rede: **10.0.0.0**
2. Broadcast:        **10.255.255.255**


Como não houve a identificação de partilha do mesmo segmento de rede entre: 
 - **10.0.0.1** e 
 - **11.0.0.1** 
há necessidade de roteamento

Dessa forma, **10.0.0.1** envia um **ARP REQUEST** perguntando o endereço do roteador:
  - quem é **10.0.0.5**?

**10.0.0.5** responde com um **ARP REPLY**
  - sou eu e **MAC Address** é tal

**10.0.0.1** envia um **ETHERNET**, cujos MAC Address são:
  - Destination MAC Address == Roteador
  -    Source   MAC Address == **10.0.0.1**

Roteador recebe **ETHERNET** advindo de **10.0.0.1**,
abre o **ETHERNET** e verifica os IP de origem e destino
  -   Source    Address == **10.0.0.1**
  - Destination Address == **11.0.0.1**

**11.0.0.1** responde
  - sou eu e **MAC Address** é tal

**10.0.0.1** responde
  - meu **MAC Address** é tal 
  - tome este Ethernet( IP(TCP) )


---

# 127.0.0.1
Rede Loopback, localizada dentro do kernel, 
iniciada a partir do módulo dentro do kernel 
que detecta a placa de rede conectada na máquina
127.0.0.1 - 127.255.255.254

# 0.0.0.0
IP desta máquina, esta máquina local

# 0.0.0.0/8
IP desta rede, 
todas as redes com as quais esta máquina tem contato neste momento
não é default gateway

# Redes Privadas
> 1 == rede | 0 == hosts
> /8 ou /12 ou /16 == número de bits ligados
```
      10        0         0         0     /8
  1111 1111 0000 0000 0000 0000 0000 0000

     172        16        0         0     /12
  1111 1111 1111 0000 0000 0000 0000 0000

     192       168        0         0     /16
  1111 1111 1111 1111 0000 0000 0000 0000
```

## Total de IPs
**OBS**: -2 pois o primeiro (rede) e o último (broadcast) são resevados
(2^8 - 2) * (2^8 - 2) * (2^8 - 2) * (2^8 - 2)

## IP Classe A
   255        0         0         0       | 10.0.0.100/255.0.0.0
   2^8       2^8       2^8       2^8      | 10.0.0.100/8
1111 1111 0000 0000 0000 0000 0000 0000   | 

## IP Classe B
   255       255        0         0       | 172.16.0.172/255.255.0.0
   2^8       2^8       2^8       2^8      | 172.16.0.172/16
1111 1111 1111 1111 0000 0000 0000 0000   |

## IP Classe C
   255       255       255        0       | 192.168.12.100/255.255.255
   2^8       2^8       2^8       2^8      | 192.168.12.100/24
1111 1111 1111 1111 1111 1111 0000 0000   |

---

# Sockets
IP + PORTA
são abstrações das camadas de rede para aplicações 
que precisam se comunicar com outras aplicações 
através de redes.

**OBS**
> Durante uma conexão, sockets do Client-Server NUNCA MUDAM \
  Caso aconteça de mudar, já é caracterizado como OUTRA conexão

Basicamente é a combinação de:
```
  protocolo + IP + porta.
```

## Endereços dos sockets
```
  /proc/*/fd/*  # File descriptors.

  /proc/net/tcp # List of TCP sockets.

  /proc/net/udp # List of UDP sockets.

  /proc/net/raw # List of raw sockets.
```

# MTU
Máxima quantidade de dados que o payload da camada dois (2) Enlace
consegue transmitir



# Roteador
Máquina que têm várias placas de rede,
cada placa de rede tem um IP,
cada IP se chama "gateway" 

## Roteamento
Roteador envia o IP para sua outra placa de rede

## Exemplo de roteamento

### Contexto
A máquina cujo IP é
- **10.0.0.1** 
quer se comunicar com a máquina cujo IP é
- **172.20.0.5**

### Digrama da rede roteada
```
              10.0.0.0                                   172.20.0.5
         MAC: 00:00:00:00:02 ───┐              ┌─── MAC: 00:00:00:00:03
          ___                   │   ________   │                  ___
         /   |                  └──|        |──┘                 |   \  
        /    |_____________________|        |____________________|    \
       /     |                     |        |                    |     \
      |______|                     |________|                    |______|
      10.0.0.1                      Roteador                    172.20.0.1
 MAC: 00:00:00:00:01                                        MAC: 00:00:00:00:04


  +--------------+      +--------------+ +--------------+     +--------------+
  |     Rede     |      |     Rede     | |     Rede     |     |     Rede     |
  +--------------+      +--------------+ +--------------+     +--------------+
  |    Enlace    |      |    Enlace    | |    Enlace    |     |    Enlace    |
  +--------------+      +--------------+ +--------------+     +--------------+
  |    Física    |      |    Física    | |    Física    |     |    Física    |
  +--------------+      +--------------+ +--------------+     +--------------+
```

> Camada de Rede faz um pacote com IP de origem e IP de destino 
+--------------+ 
|    Camada    |   +--------+----------------------------------------------+ 
|      de      |   | header | IP origem: 10.0.0.1 | IP destino: 172.20.0.5 |
|     Rede     |   +--------+----------------------------------------------+ 
+--------------+ 

> Camada de Enlace encapsula o IP dentro de um frame (quadro) Ethernet e o envia para o roteador
+--------------+ 
|    Camada    |   +--------+------------------------------------------------------------------------------+ 
|      de      |   | header | Destination MAC Address: 00:00:00:00:02 | Source MAC Address: 00:00:00:00:01 |
|    Enlace    |   +--------+------------------------------------------------------------------------------+ 
+--------------+ 

> Camada Física envia bits
+--------------+ 
|    Camada    |      BITS
|    Física    | 
+--------------+ 



+------------------------------- DENTRO DO ROTEADOR -----------------------------+

IP Address (Endereço de Rede)
  - se mantém até o final

MAC Address (Endereço de Enlace)
  - troca, não transpõe roteador, faz-se necessário fazer um novo


> Camada Física recebe bits
```
+--------------+    
|    Camada    |      BITS
|    Física    |    
+--------------+    
```

> Camada de Enlace confere Destination MAC Address e, caso seja o igual, abre o frame (quadro) Ethernet
```
+--------------+    
|    Camada    |   +--------+------------------------------------------------------------------------------+ 
|      de      |   | header | Destination MAC Address: 00:00:00:00:02 | Source MAC Address: 00:00:00:00:01 |
|    Enlace    |   +--------+------------------------------------------------------------------------------+ 
+--------------+   
```

> Camada de Rede recebe um pacote com IP e o roteador envia o IP para sua outra placa de rede (roteamento)
```
+--------------+    
|    Camada    |   +--------+----------------------------------------------+   
|      de      |   | header | IP origem: 10.0.0.1 | IP destino: 172.20.0.5 |
|     Rede     |   +--------+----------------------------------------------+  
+--------------+ 
```


> Camada de Rede cria um novo pacote com IP de origem e IP de destino, advindo da outra placa de rede do roteador
```
+--------------+    
|    Camada    |   +--------+----------------------------------------------+   
|      de      |   | header | IP origem: 10.0.0.1 | IP destino: 172.20.0.5 |
|     Rede     |   +--------+----------------------------------------------+  
+--------------+ 
```

> Camada de Enlace encapsula o IP dentro de um frame (quadro) Ethernet e o envia para a máquina de destino
```
+--------------+    
|    Camada    |   +--------+------------------------------------------------------------------------------+ 
|      de      |   | header | Destination MAC Address: 00:00:00:00:04 | Source MAC Address: 00:00:00:00:03 |
|    Enlace    |   +--------+------------------------------------------------------------------------------+  
+--------------+   
```

> Camada Física envia bits
```
+--------------+    
|    Camada    |     
|      de      |      BITS
|    Física    |    
+--------------+    
```

+------------------------------- DENTRO DO ROTEADOR -----------------------------+



> Camada Física recebe bits
```
+--------------+    
|    Camada    |      
|      de      |      BITS
|    Física    |    
+--------------+    
```

> Camada de Enlace confere Destination MAC Address e, caso seja o igual, abre o frame (quadro) Ethernet
```
+--------------+    
|    Camada    |   +--------+------------------------------------------------------------------------------+ 
|      de      |   | header | Destination MAC Address: 00:00:00:00:04 | Source MAC Address: 00:00:00:00:03 |
|    Enlace    |   +--------+------------------------------------------------------------------------------+ 
+--------------+   
```

> Camada de Rede recebe um pacote com IP e a máquina destino agora sabe o circuito até a máquina de origem
```
+--------------+    
|    Camada    |   +--------+---------------------------------------------+   
|      de      |   | header |IP origem: 10.0.0.1 | IP destino: 172.20.0.5 |
|     Rede     |   +--------+---------------------------------------------+  
+--------------+
```


# Switch
Pode-se dizer, que é uma Bridge com muitas portas

Switch respeita o protocolo:
- se for unicast -> Switch funciona em Unicast
- se for Multicast -> Switch funciona em Multicast
- se for Broadcast -> Switch funciona em Broadcast
Funciona em unicast quando um IP quer falar com outro IP
- 10.0.0.1
- 10.0.0.2
No exemplo acima, o Switch funcionará como unicast:
- Vai fazer com que o saia do 10.0.0.1 e entre somente no 10.0.0.2

No caso de ARP, sai de uma porta e entra em todas as outras
- 10.0.0.1
A máquina **10.0.0.1** envia um ARP, que vai para todos no segmento de rede:
- 10.0.0.2
- 10.0.0.5



# Bridge
Máquina com duas placas de rede e que trabalha na camada 2,
como se fosse um switch

Realiza a interligação entre duas porções de via camada 2

## Bridge: principais usos
- Interligação de duas porções do mesmo segmento de rede
- Conversão de protocolos de camada 2
- Elemento de auditoria e análise de tráfego
- Base para elementos de firewall

## Bridge: como criar
[Bridge Debian](http://bit.ly/bridge_debian)

## Conecte
In TigerVNC:
  - 127.0.0.1

## Bridge Install (Debian)
* Pacote para formalizar uma bridge dentro do Debian
```
  apt install bridge-utils
```

* Mostre as bridges
```
  brctl show
```

* Adicione uma bridge
```
  brctl addr br0
```

* Adicione interfaces a uma bridge
```
  brctl addif br0 eth0
  brctl addif br0 eth1
```

* Suba uma bridge
```
  ifconfig br0 up
  ip link set br0 up
```


# Gateway
IP em outra máquina que leva-te para outro segmento de rede,
outra rede, vulgarmente

É configurado numa máquina que permitirá a comunicação
entre segmentos de rede diferentes

Gateway
 - 192.168.10.1

Máquina 1
 - 192.168.10.2
  Gateway
   - 192.168.10.1

Máquina 2
 - 192.168.10.3
  Gateway
   - 192.168.10.1
   
Máquina 3
 - 192.168.11.2
  Gateway
   - 192.168.11.1
---

# Mascará de Rede
São para seres humanos

A máscara de rede é equivalente a CIDR (/8, /16, /24),
mas em CIDR é representando o número de bits ligados,
já a máscara representa em decimal

# Sub Net
Vamos realizar um exemplo de sub-net
Usaremos o endereço classe C: **192.168.86.0/24**

## Dados iniciais
   IP base
192.168.86.0/24

   IP rede   | Intervalo de IPs utilizáveis |  IP broadcast
192.168.86.0 |        192.168.1-254         | 192.168.86.255

   máscara   | CIDR
255.255.255.0|  /24

## Explanação do exemplo
O exemplo será realizado em uma divisão de **3 redes**.

### 0º Identificar o número de IPs utilizáveis
Como o endereço é de classe C, tem-se 8 bits desligados
```
   255       255       255        0    
   2^8       2^8       2^8       2^8   
1111 1111 1111 1111 1111 1111 0000 0000
```
Para deixar ainda mais identificável: 
```
    0    
   2^8   
0000 0000
```
Dessa forma, o total de endereços IPs utilizáveis é: 
```
  2^8 == 256
```

### 1º Ligar bit mais significativo
#### 1.1º
O bit mais significativo da parte exclusiva de hosts, será ligado
```
    0    
   2^8   
1000 0000
```
Com isso, acabou-se de criar uma nova rede. 

#### 1.2º
Como se deseja criar 3 redes e agora só é possível 2 redes,
liga-se mais um bit.
```
    0    
   2^8   
1100 0000
```
Com isso, acabou-se de criar mais 2 novas redes. 
Contudo, deseja-se usar apenas 3 redes no máximo. 
Então, a quarta rede não é utilizada. 

#### 1.1º Aplicar nova numeração de bit à regra do intervalo
Como o bit mais significativo (mais à esquerda do número) 
foi acionado, faz-se necessário saber o novo número de hosts
```
128  64  32  16  8  4  2  1
  1   1   0   0  0  0  0  0
```
Agora, o novo número de hosts (da máscara) é de **192** possibilidades.
```
128 + 64 = 192
```
Uma vez que um bit (mais à esquerda) foi acionado para a rede
```
   255       255       255       128    
   2^8       2^8       2^8       2^8   
1111 1111 1111 1111 1111 1111 1000 0000
```
Note que o intervalo de endereços caiu pela metade:
```
  2^8 == 256
  2^7 == 128

  256 - 128 = 128
```
Como o exemplo liga dois bits, 
```
   255       255       255       128    
   2^8       2^8       2^8       2^8   
1111 1111 1111 1111 1111 1111 1100 0000
```
o intervalo de endereços foi divido por 4:
```
  2^8 == 256
  2^7 == 128
  2^6 == 64

  256 - 128 - 64 = 64
  256 / 4 = 64
```

### 2º Identificar novos dados das redes criadas
Como já foram criadas duas redes, chegou a hora de identificar
os novos dados referentes a essas duas redes

#### 2.1º Primeira rede
   IP base
192.168.86.0/26

   IP rede   | Intervalo de IPs utilizáveis |  IP broadcast
192.168.86.0 |        192.168.1-62         | 192.168.86.63

   máscara      | CIDR
255.255.255.192 |  /26

#### 2.2º Segunda rede
   IP base
192.168.86.0/26

   IP rede     |  Intervalo de IPs utilizáveis  |  IP broadcast
192.168.86.64  |        192.168.65-126          | 192.168.86.127

   máscara      | CIDR
255.255.255.192 |  /26

#### 2.3º Terceira rede
   IP base
192.168.86.0/26

   IP rede      |  Intervalo de IPs utilizáveis  |  IP broadcast
192.168.86.128  |        192.168.129-190         | 192.168.86.191

   máscara      | CIDR
255.255.255.192 |  /26

#### 2.4º Quarta rede
   IP base
192.168.86.0/26

   IP rede      |  Intervalo de IPs utilizáveis  |  IP broadcast
192.168.86.192  |        192.168.193-254         | 192.168.86.255

   máscara      | CIDR
255.255.255.192 |  /26

# OBS  
O total de sub-redes, pode ser calculado ao inverso do caminho
de bits
```
128  64  32  16  8  4  2  1
  0   0   0   0  0  0  0  0
```
Conforme liga-se o bit mais significativo (mais à esquerda),
aumenta-se o número de sub-redes referentes a rede inicial.

## Uma rede
```
1   2   4   8  16  32  64  128
0   0   0   0   0   0   0    0
```

## Duas sub-redes
```
1   2   4   8  16  32  64  128
1   0   0   0   0   0   0    0
```

## Quatro sub-redes
```
1   2   4   8  16  32  64  128
1   1   0   0   0   0   0    0
```

---

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
```

Abre uma porta local
* -l == lista a porta
* -k == não mata a porta depois da conexão
```
  nc -l -k <PORT>
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

Captura dois pacotes IP (segmento ICMP)
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
* host      = IP capturado
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
* IP == IP para qual será mandado
* -d == rede e host a ser enviado
* -F == Flags: (S)YN, (P)USH, (R)ESET
```
  packit -d <IP> -F SPR
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

* exibe IP com MAC Address
```
  ip n # equivalente a: arp -n
```

* exibe as rotas que os pacotes terão de tomar, pelo gateway  
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

Possui um número de identificação (id) - que não muda,
e um número de sequẽncia - este muda.

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
  apt    install install docker.io tigervnc-viewer
  zypper in      install docker.io tigervnc-viewer
```
## Execute o Docker
```
  docker container run -d --cap-add=NET_ADMIN --cap-add=SYS_ADMIN -p 5900:5900 -p 8080:8080 d3f0/coreemu_vnc
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
IPTABLES, bloqueie tudo que vier para a porta 81 desta máquina
* -A || --append   INPUT == esta máquina
* -p || --protocol tcp   == protocolo
* --dport                == porta
* -j || --jump     DROP  == descarte
```
  iptables -A INPUT -p tcp --dport 81 -j DROP
```

## HOST
Demonstra DNS e IP
* -4  = retorna IPv4
```
  host -4 myip.opendns.com resolver1.opendns.com
  curl ifconfig.me
```

---

# DHCP
Fornece dados de rede: IP, Gateway, Mascará

Quando não se esta numa rede onde se conhece, não se administra
atribuí-se um IP dinamicamente.

Existem duas forma de receber DHCP:
- direto no MAC Address
- ou em Broadcast (o número de identificação (id) que vai e volta)

Usa-se o protocolo DHCP, 
através do cliente DHCP instalado na máquina
para obter do servidor DHCP da rede 
quais as configurações de rede a serem utilizadas

## RFC DHCP
> 2131 -> 3315

## Exemplo do protocolo IP: tipo DHCP
```
  header  IP
  payload IP { 
    header DHCP
    payload DHCP
  }
```


## Estrutura do DCHP
```
     0                   1                   2                   3
   0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |     op (1)    |   htype (1)   |   hlen (1)    |   hops (1)    |
   +---------------+---------------+---------------+---------------+
   |                            xid (4)                            |
   +-------------------------------+-------------------------------+
   |           secs (2)            |           flags (2)           |
   +-------------------------------+-------------------------------+
   |                          ciaddr  (4)                          |
   +---------------------------------------------------------------+
   |                          yiaddr  (4)                          |
   +---------------------------------------------------------------+
   |                          siaddr  (4)                          |
   +---------------------------------------------------------------+
   |                          giaddr  (4)                          |
   +---------------------------------------------------------------+
   |                                                               |
   |                          chaddr  (16)                         |
   |                                                               |
   |                                                               |
   +---------------------------------------------------------------+
   |                                                               |
   |                          sname   (64)                         |
   +---------------------------------------------------------------+
   |                                                               |
   |                          file    (128)                        |
   +---------------------------------------------------------------+
   |                                                               |
   |                          options (variable)                   |
   +---------------------------------------------------------------+
```
---

# Estrutura do Protocolo
Protocolo == modo como as coisas vão acontecer
Conjunto de regras literais, que estabelecem um padrão
de comunicação e comportamento
> Tem (uma implementação do) protocolo IP passando na tela
```
  header  (cabeçalho)
  payload (área de dados)
```

## Exemplo do protocolo IP: tipo TCP, tipo http
> No transporte, só é visível o IP (Boneca Russa)
```
  header  IP
  payload IP { 
    header TCP
    payload TCP {
      http
    }
  }
```

> Contextualização
```
  Ethernet  == agẽncia de distribuição
  IP        == é enviado ao número da casa
  TCP       == uma vez dentro da casa, é enviado às portas do lado de dentro da casa
```

---

# ETHERNET
Nome da tecnologia é Ethernet, em função da comparação com Eter.
Antigamente, enviava-se um sinal e preenchia a rede muito rápida.
Como o Eter, que preenche o ar muito rápido.

Protocolo usado na camada de Enlace (camada dois), do Modelo OSI
* Destination MAC Address == primeiro vem o destino, 
                             para o que o switch, 
                             já tendo recebido o frame Ethernet
                             reenvie-o para outro switch
* EtherType == definição do tipo Ethernet (ARP, IPv6, IPv4 etc.)
               que está dentro payload
* Payload == carrega o frame (tipo de protocolo) Ethernet
             46 é um número que, somado ao header (14) e ao checksum (4)
             da 64 bytes, a menor unidade de transmissão sem perda de qualidade
             46 + 14 + 4 = 64
             caso IP tenha menos de 46 bytes, o resto será completado com zeros (0)
             o valor 1500, deflagra o motivo do IP (v4, v6) possuir,
             no máximo, 1500 bytes, por ser o máximo de payload do frame (quadro) Ethernet
* CRC Checksum == carrega o checksum do frame Ethernet 
```
                                  Frame (quadro) Ethernet tipo 2
                                        (64 - 1518 bytes)
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  __________________________ _____________________ ___________   _________________    _________________  | 
| |     80 00 20 7a 3f 3e    |  80 00 20 20 3a ae  |   08 00   | |   IP, ARP etc.  |  |   00 20 20 3a   | | 
| |                          |                     |           | |                 |  |                 | | 
| | Destination MAC Address  | Source MAC Address  | EtherType | |     Payload     |  |  CRC Checksum   | | 
| |__________________________|_____________________|___________| |_________________|  |_________________| | 
|                            MAC HEADER                                 DATA                              | 
|                           ( 14 bytes )                          (46 - 1500 bytes)        (4 bytes)      | 
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

```
 
## Valores da transmissão
- Ethernet:      10         MBPS
- Fast Ethernet: 100        MBPS
- Gigabit:       1000       MBPS
- 10 Gigabit:    10.000     MBPS

---

# IP
Internet Protocolo (Protocolo Internet)
largura do TCP/IP (linha) = 32 bits ou 4 bytes

IP é barato na rede, já o TCP é caro

Em geral, IPv4 funciona em 
- Unicast
mas pode funcionar também em:
- Broadcast
- Multicast

Já o IPv6, pode funcionar em 
- Unicast
- Anycast
- Multicast


## Estrutura Cabeçalho IP
```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Version|  IHL  |Type of Service|          Total Length         |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         Identification        |Flags|      Fragment Offset    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Time to Live |    Protocolo  |         Header Checksum       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                       Source Address                          |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Destination Address                        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options                    |    Padding    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

```

## IPv6
Pelo fato de qualquer protocolo IP (TCP, UDP, ICMP etc.)
garantir os dados primordiais do IP 
- em função do cálculo de checksum (do TCP, UDP, ICMP etc.) -
o IPv6 não possui checksum

## Menor IP 
O menor IP possível de ser enviado, é composto por:
20 bytes do cabeçalho obrigatório + 1 byte de payload

## Cabeçalho

### Version
Composto por um campo de tamanho igual a 4 bits
Em geral, setado: 0100 -> 4

### IHL (Internet Header Length, Tamanho do Cabeçalho Internet)
Composto por um campo de tamanho igual a 4 bits

15 linhas (15 * 4 bytes = 60 bytes)
cada linha tem no mínimo 4 bytes (32 bits)

5 (5 * 4 bytes = 20 bytes) primeiras linhas: obrigatórias

10 (10 * 4 bytes = 40 bytes) em seguida:     opcionais

### Total Length
Tamanho em bytes de TODO o IP
Composto por um campo de tamanho igual a 16 bits
Podendo transmitir até 65.535 bytes

### Indetification
Identificação dos fragmentos de mensagem
Composto por um campo de tamanho igual a 16 bits
onde um número (segundo a RFC 791) aleatório deve ser gerado pelo OS
e os pacote deve ser enviado:
  cabeçalho + payload
    20      + max_suportado_pela_placa_de_rede(len(payload))
#### Perguntas
Chegaram na ordem?
Tem mais algum para chegar?
Qual a ordem de remontagem?

### Flag
Composto por um campo de tamanho igual a 3 bits
  None
  Dont Fragment
  More Fragment

### Time To Live (ttl)
Tempo de vida de um pacote
Composto por um campo de tamanho igual a 8 bits

### Protocol
IP só armazena outros protocolos, os protocolos IP
  ```
  /etc/protocols
  /usr/etc/protocols
  c::\windows\system\drivers/etc/protocols
```

### Header Checksum
Calcula o checksum do cabeçalho IP
Composto por um campo de tamanho igual a 16 bits
Seu calculo de dá (em Hexadecimal): 
  soma de 2 em 2 bytes do cabeçalho, menos os 2 do checksum
  coloca um 00 na frente do resultado
  soma os 2 bytes do lado esquerdo com os 2 bytes do lado direito
  verifica complemento -> subtrai de FF FF

#### Exemplo de calculo de Checksum
* . == não faz parte do cabeçalho
* terceira linha, terceiro e quarto bytes == 06e5 == checksum
```
 0x0000:  4500 0148 450c 4000 4011 06e5 c0a8 3602
 0x0010:  c0a8 3661 .... .... .... .... .... ....
```

* soma de 2 em 2 bytes do cabeçalho, menos os 2 do checksum
```
  4500 + 0148 + 450c + 4000 + 4011 + c0a8 + 3602 + c0a8 + 3661
```

* coloca um 00 na frente do resultado
```
  2 f9 18 -> 02 f9 18 -> 00 02 f9 18
```

* soma os 2 bytes do lado esquerdo com os 2 bytes do lado direito
```
  00 02 + f9 18 -> f9 1a
```

* verifica complemento -> subtrai de FF FF
```
  ff ff - f9 1a -> 06 e5
```

### Source Address
Endereço IP de origem, da máquina que envia IP

### Destination Address
Endereço IP de destino, da máquina que receberá IP

## Exemplo de Captura de IP
- OBS: Valores em hexadecimal

* -n 				= não resolve nome
* ip 				= ipv4
* -c <NUM> 	= pacotes
* -x 				= hexadecimal
```
  sudo tcpdump -n ip -c 1 -x 
```

> Resultado do tcpdump
```
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on enp2s0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
17:24:19.894567 IP 192.168.54.2.68 > 192.168.54.97.67: BOOTP/DHCP, Request from f0:4d:a2:e0:2c:c9, length 300
        0x0000:  4500 0148 450c 4000 4011 06e5 c0a8 3602
        0x0010:  c0a8 3661 0044 0043 0134 eef9 0101 0600
        0x0020:  ecff 7636 0000 0000 c0a8 3602 0000 0000
        0x0030:  0000 0000 0000 0000 f04d a2e0 2cc9 0000
        0x0040:  0000 0000 0000 0000 0000 0000 0000 0000
        0x0050:  0000 0000 0000 0000 0000 0000 0000 0000
        0x0060:  0000 0000 0000 0000 0000 0000 0000 0000
        0x0070:  0000 0000 0000 0000 0000 0000 0000 0000
        0x0080:  0000 0000 0000 0000 0000 0000 0000 0000
        0x0090:  0000 0000 0000 0000 0000 0000 0000 0000
        0x00a0:  0000 0000 0000 0000 0000 0000 0000 0000
        0x00b0:  0000 0000 0000 0000 0000 0000 0000 0000
        0x00c0:  0000 0000 0000 0000 0000 0000 0000 0000
        0x00d0:  0000 0000 0000 0000 0000 0000 0000 0000
        0x00e0:  0000 0000 0000 0000 0000 0000 0000 0000
        0x00f0:  0000 0000 0000 0000 0000 0000 0000 0000
        0x0100:  0000 0000 0000 0000 6382 5363 3501 0337
        0x0110:  1701 1c03 791a 0c0f 7706 2829 5755 562c
        0x0120:  2d2e 2f2a f921 fc11 ff00 0000 0000 0000
        0x0130:  0000 0000 0000 0000 0000 0000 0000 0000
        0x0140:  0000 0000 0000 0000
1 packet captured
1 packet received by filter
0 packets dropped by kernel

```

> Na resposta, os dois-pontos (:) e espaço em seguida, separa protocolos

### Primeira linha do IP
* 4500 0148
1. 45 == Primeiro Byte (4 == Version | 5 == IHL [total linhas do cabeçalho] )
2. 00 == Segundo  Byte (Type of Service)
2. 01 == Terceiro Byte (Total Length [tamanho total do IP] ) 0148 (HEX) == 296 (Dec) Bytes
4. 48 == Quarto   Byte

### Segunda linha do IP
* 450c 4000
1. 45 == Quinto Byte (Número de identificação == 450c (HEX) == 17676 (Dec) )
2. 0c == Sexto  Byte
3. 40 == Sétimo Byte (3 primeiros bits == Flags | 4-16 bits == Fragment of Set [para caso haja fragmentação] )
4. 00 == Oitavo Byte (4000 (HEX) == 0100 0000 0000 0000 | 010 [None, Dont Fragment, More Fragment] == Não fragmente)

### Terceira linha do IP
* 4011 06e5
1. 40 == Nono Byte            (TTl: 40 (HEX) == 64 (Dec) )
2. 11 == Décimo  Byte         (Protocol: 11 (HEX) == 17 (Dec) == UDP)
2. 06 == Décimo Primeiro Byte (Checksum)
4. e5 == Décimo Segundo Byte

### Quarta linha do IP ( SRC [Endereço de Origem] )
* c0a8 3602
1. c0 == Décimo Terceiro Byte -> c0 (Hex) == 192 (Dec)
2. a8 == Décimo Quarto   Byte -> a8 (Hex) == 168 (Dec)
3. 36 == Décimo Quinto   Byte -> 36 (Hex) == 54  (Dec)
4. 02 == Décimo Sexto    Byte -> 02 (Hex) == 2   (Dec)

### Quinta linha do IP ( Destination [Endereço de Destino] )
* c0a8 3661
1. c0 == Décimo Sétimo Byte -> c0 (Hex) == 192 (Dec)
2. a8 == Décimo Oitavo Byte -> a8 (Hex) == 168 (Dec)
3. 36 == Décimo Nono   Byte -> 36 (Hex) == 54  (Dec)
4. 61 == Vigésimo      Byte -> 61 (Hex) == 97  (Dec)

### Sexta linha do IP ( Começo do próximo cabeçalho )
* OBS: o IP capturado foi um UDP
* 0044 0043
1. 00 == Vigésimo Primeiro Byte -> 00 (Hex) == 00 (Dec) == UDP PORT Src
2. 44 == Vigésimo Segundo  Byte -> 44 (Hex) == 68 (Dec)
3. 00 == Vigésimo Terceiro Byte -> 00 (Hex) == 00 (Dec) == UDP PORT Destination
4. 43 == Vigésimo Quarto   Byte -> 43 (Hex) == 67 (Dec)

---

# TCP
Protocolo orientado a conexão, 
pois verifica a conexão antes de enviar dados
através do Three-Way Handshake

É disparado contra uma porta, já estando dentro da máquina final

5 (5 * 4 bytes = 20 bytes) primeiras linhas = obrigatórias

10 (10 * 4 bytes = 40 bytes) em seguida     = opcionais

15 linhas (15 * 4 bytes = 60 bytes)         = máximo de linhas

TCP é caro ao ser transmitido pela rede

**OBS**
> Qualquer host numa rede TCP/IP, deve aceitar, no mínimo, 576 bytes (64 header, 512 palyoad)


**OBS**
> TCP transporta segmento, SEGMENTO.


**OBS**
> Quando o segmento TCP não obtém resposta, o TCP RETRANSMITE o segmento.
  Isto é, mesmas: 
    * socket (IP+Port) origem
    * socket (IP+Port) destino
    * Flag
    * seq
    * window 
    * options
    * length

## Aplicação para TCP
O TCP é controlado pela aplicação, 
pois a aplicação não sabe fazer o que o TCP faz.

Caso a porta esteja fechada, isso pode significar que a aplicação
saiu do ar.

### EX 1
```
Firefox (General) diz:
  - TCP, conecte com a porta 80 dessa outra máquina
  - e fale para ela: GET /

TCP fala a outra máquina:
  - SYN

Porta 80 da outra máquina:
  - ACK

  .
  .
  .

TCP fala para Firefox:
  - Tome a resposta

Firefox (General):
  - Resposta recebida
```

### EX 1
```
Apache (Servidor WEB)
  - TCP, abra uma porta 80
  - e fique "escutando"

  .
  .
  .

Apache (Servidor WEB)
  - TCP, feche a porta 80
```

**OBS**
> ao passar um número de uma porta que não existe, SERVER envia um RST (Reset == "não entendi")

## Estrutura do cabeçalho TCP
> Primeiras 5 linhas são obrigatórias
```
 0            7               15            23                31
-----------------------------------------------------------------
|          source port          |       destination port        |
-----------------------------------------------------------------
|                        sequence number                        |
-----------------------------------------------------------------
|                     acknowledgment number                     |
-----------------------------------------------------------------
|  HL   | rsvd  |C|E|U|A|P|R|S|F|       window size             |
-----------------------------------------------------------------
|         TCP checksum          |       urgent pointer          |
-----------------------------------------------------------------
|                    options                  |     padding     |
-----------------------------------------------------------------

```

## Sequence Number
O número de sequência, marca cada byte do payload.
Então, pelo tamanho do payload, é possível ter
um número de sequência para cada byte desse tamanho.

Iniciamente é aleatório, mas se torna sequencial durante a conexão


### Sequence Number Absolute
O tcpdump possui duas forma de mostrar o número de sequência
```
  tcpdump -n -r <FILE>.pcap -S
```
> -S == mostra o número de sequência completo

### Sequence Number Relative
O tcpdump possui duas forma de mostrar o número de sequência
```
  tcpdump -n -r <FILE>.pcap
```
Mostra o número de sequência nos SYN iniciais
Em seguida, soma ao número de sequência anterior uma unidade

#### Exemplo de sequence number relative no tcpdump
```
  2022-05-06 11:04:31.102796 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [S], seq 810775634, win 65495, options [mss 65495,sackOK,TS val 2518909665 ecr 0,nop,wscale 7], length 0
  2022-05-06 11:04:31.102830 IP 127.0.0.1.1234 > 127.0.0.1.44980: Flags [S.], seq 1555075220, ack 810775635, win 65483, options [mss 65495,sackOK,TS val 2518909665 ecr 2518909665,nop,wscale 7], length 0
  2022-05-06 11:04:31.102855 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [.], ack 1, win 512, options [nop,nop,TS val 2518909665 ecr 2518909665], length 0
  2022-05-06 11:05:25.591261 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [P.], seq 1:6, ack 1, win 512, options [nop,nop,TS val 2518964153 ecr 2518909665], length 5
```
> SERVER
* 127.0.0.1.1234 == seq 1555075220
* 127.0.0.1.1234 == seq 1:6 (1555075220 + 1 == 1555075221 | 1555075220 + 6 = 1555075226)


### Exemplo de análise de número de sequência
> Comando para gerar o arquivo
```
  sudo tcpdump -ni lo -v -w <FILE>.pcap
```

> Comando para exibir saída do arquivo, com número de sequência absoluto
```
  sudo tcpdump -n -r <FILE>.pcap -S
```

Saída do tcpdump, com número de sequência absoluto
Apenas a primeira linha e algumas linhas com RST (Reset), 
sempre existirá um ack (representado por um pontinho)
```
  tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
  listening on lo, link-type EN10MB (Ethernet), snapshot length 262144 bytes

  2022-05-06 11:04:31.102796 IP 127.0.0.1.44980 > 127.0.0.5.80: Flags [S], seq 810775634, win 65495, options [mss 65495,sackOK,TS val 2518909665 ecr 0,nop,wscale 7], length 0

  2022-05-06 11:04:31.102830 IP 127.0.0.5.80 > 127.0.0.1.44980: Flags [S.], seq 1555075220, ack 810775635, win 65483, options [mss 65495,sackOK,TS val 2518909665 ecr 2518909665,nop,wscale 7], length 0

  2022-05-06 11:04:31.102855 IP 127.0.0.1.44980 > 127.0.0.5.80: Flags [.], ack 1555075221, win 512, options [nop,nop,TS val 2518909665 ecr 2518909665], length 0

  2022-05-06 11:04:31.102855 IP 127.0.0.1.44980 > 127.0.0.5.80: Flags [P.], seq 810775635:810775642, ack 1, win 512, options [nop,nop,TS val 2518909665 ecr 2518909665], length 7: HTTP: GET /
```

#### Interpretação da saída
CLIENT conecta ao server 
Flag: SYN
seq:  meu número de sequência (iniciamente aleatório): seq 810775634
```
  IP 127.0.0.1.44980 > 127.0.0.5.80: Flags [S] seq 810775634
```

SERVER responde ao CLIENT: 
Flag: ACK-SYN
seq:  meu número de sequência é: seq 1555075220
ack:  espero que seu próximo número de sequência enviado seja: ack 810775635
```
  IP 127.0.0.5.80 > 127.0.0.1.44980: Flags[S.] seq 1555075220, ack 810775635
```

CLIENT responde ao SERVER:
Flag: ACK. 
seq:  como Ack não é Flag, não possui número de sequência
ack:  espero que seu próximo número de sequência enviado seja: ack 1555075221
```
  IP 127.0.0.1.44980 > 127.0.0.5.80 Flags [.], ack 1555075221
```

CLIENT responde ao SERVER:
Flag: ACK-PSH (Push)
seq:  meu número de sequência é: seq 810775635
ack:  espero que seu próximo número de sequência enviado seja: ack 1555075221
```
  IP 127.0.0.1.44980 > 127.0.0.5.80: Flags [P.], seq 810775635:810775642, ack 1555075221, length 7: HTTP: GET /
```
> Foi enviado um Psuh com GET /
> Push tem número de sequência: 810775635 <- o mesmo que o SERVER espera
> Como se tem um número de sequência para cada byte do payload e o tamanho do payload é 7
> 810775635 + 7 = 810775642 <- próximo número de sequência esperado pelo SERVER
> 810775642 não está escrito dentro do header TCP, é uma dedução matemática
> length 7, também é dedução matemática do tcpdump


## Acknowledgment Number
Número de sequência que se espera receber, na próxima vez


## Procedimentos (também são conhecidos como Flags)
**OBS**: procedimentos não possuem número de sequência, apenas Flags possuem.
Urg (urgent)         =
Ack (acknowledgment) = confirmação de que é conhecido o número de sequência do próximo segmento a ser enviado pelo lado oposto

## Flags
CWR (Congestion Window Reduced) = ECE bit foi recebido, janela de congestionamento foi reduzida.
ECE (ECN-Echo)                  = bit CE foi recebido. notificação explicita de congestionamento
Psh (push)                      = envia dados        -> único com payload (área de dados)
Rst (reset)                     = "não entendi"
Syn (syncronize)                = inicia conexões
Fin (Finsh)                     = finaliza conexões

## Exemplo de comunicação Three-Way-Handshake
```
  Client -> Server SYN

  |C|E|U|A|P|R|S|F|
  |---------------|
  |0 0 0 0 0 0 1 0|
  |---------------|
  |7 6 5 4 3 2 1 0|

  Server -> Client ACK Server -> Client SYN

  |C|E|U|A|P|R|S|F|
  |---------------|
  |0 0 0 1 0 0 1 0|
  |---------------|
  |7 6 5 4 3 2 1 0|

  Client -> Server ACK

  |C|E|U|A|P|R|S|F|
  |---------------|
  |0 0 0 1 0 0 0 0|
  |---------------|
  |7 6 5 4 3 2 1 0|

```

## Formas de Finalizar uma conexão
### 1/2 (Meio) Fechamento
> Fechamento pode ser iniado pelo Client ou pelo Server
```
FYN       <- Envia fechamento
ACK       <- Confirma que recebeu o fechamento
FYN       <- Envia fechamento
ACK       <- Confirma que recebeu o fechamento
```

### Fechamento Completo
```
FYN       <- Envia fechamento
ACK/FYN   <- Diz que recebeu o fechamento e fecha este lado
ACK       <- Confirma que recebeu o fechamento (não pode enviar mais nada)
```

## Retransmissão
TCP é um protocolo que reenvia um determinado segmento,
caso o não tenha obtido uma resposta satisfatória ao seu envio


### Reetransmissão Rápida
Envia-se um TCP/IP, num determinado tempo (Initial Time Out | ITO)
caso não tenha chegado, manda-se novamente um TCP (dentro de outro IP)
com o dobro do tempo (em relação ao TO) em relação ao anterior

ITO é o valor inicial de envio do pacote, que hoje vale 1 segundo.

O valor do Time Out (TO) é calculado a partir de valores contidos dentro do campo options
```
options [..., TS val <NUM> ecr <NUM>, ...]
```
> TS val <NUM> == Time Stamp, tempo (em milisegundos) decorrido desde algum ponto
> ecr <NUM> == Echo Reply, retorno do mesmo tempo enviado, só que pelo outro lado da conexão

Com esses valores, as máquinas (CLIENT-SERVER) conhecem o tempo 
para os segmentos poderem ir e voltar (Time Stamp - ECR).

A partir disso, as máquinas podem realizar um calculo matemático
para estabelecer um valor de Time Out (TO) confiável para agora.


### Reetransmissão A Pedido
Quando um número de sequência TCP de um lado da conexão 
(Acknowledgment Number)
não é o mesmo número de sequência esperado pelo outro lado da conexão,
entende-se que o pedido requisitado não foi recebido

Nesse sentido, o TCP reetransmitite


## Detectáveis
* quando há muito reset, algo está errado na conexão
```
Rst <- por exemplo, alguém bateu numa porta inexistente, ou fechada
```

* porta fechada e aplicação que abria a porta via TCP, estava DOWN
```
CLIENT -> SERVER (SYN)
SERVER -> CLIENT (RST)
```

* quando há SYN reetransmitidos, bloqueio na ida ou na volta
```
Syn <- aplica-se tcpdump ao longo da topologia (Syn-nada)
``` 


## Exemplo de Captura de TCP/IP
- OBS: Valores em hexadecimal

* -n 				= não resolve nome
* -i 				= interface expecífica
* lo 				= interface usada: loopback
* port 			= porta
* or 			  = uma porta ou outra
```
  sudo tcpdump -ni lo port 80 or port 81
```

> Resultado do tcpdump
```
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on lo, link-type EN10MB (Ethernet), capture size 262144 bytes
17:53:57.490222 IP 127.0.0.1.47480 > 127.0.0.5.80: Flags [S], seq 3874719047, win 65495, options [mss 65495, sackOK,TS val 3321501179 ecr 0,nop,wscale 7], length 0
```

### Interpretação
```
Client (127.0.0.1.47480) fala ao Server (127.0.0.5.80)
  - SYN

  - win 65495
  window size
  Quando você for mandar alguma coisa, não mande mais de: 65495 bytes
  Isso é uma reserva de buffer.
  Em geral, começa com número baixo e vai crescendo até estabilizar

  - options [mss 65495, sackOK,TS val 3321501179 ecr 0,nop,wscale 7]
   - wscale == sempre vem na linha SYN, potencializa janela de bytes 
               para as próximas janelas que NÂO sâo SYN
               win <NUM> ^ wscale -> win 512 ^ wscale 7 -> win 512 ^ 7 bytes (não mande mais de)

  - length 0
  Como não existe payload, o tamanho é zero
```
---

# UDP
A aplicação, que roda ao lado do processador, 
fará checagem do que o UDP não faz.
```
 0      7 8     15 16    23 24    31
+--------+--------+--------+--------+
|      source     |    Destination  |
|       port      |       port      |
+--------+--------+--------+--------+
|                 |                 |
|      Length     |     Checksum    |
+--------+--------+--------+--------+

```

**OBS**
Como qualquer host numa rede TCP/IP, deve aceitar, no mínimo, 576 bytes (64 header, 512 palyoad)
os pacotes UDP tendem a ser, no máximo, deste tamanho (576 bytes)


**OBS**
> UDP transporta segmento, SEGMENTO.


Como não possui Flags, não se auto controla, dependendo assim, 
do ICMP para isso. Veja o exemplo abaixo:

## Exemplo de Captura de UDP/IP

```
  tcpdump -ni lo
```

> -u == use UDP
```
  nc -u 127.0.0.5 632   <- 632, porta que não existe
  teste                 <- enviado via UDP
```

> Resultado do tcpdump
```
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on enp2s0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
18:27:45.865639 IP 127.0.0.1.52506 > 127.0.0.5.632: UDP, length 6
18:27:45.865639 IP 127.0.0.5 > 127.0.0.1: ICMP 127.0.0.5 udp port 632 unreachable, length 42
```
> Server responde com ICMP (somente o TCP não depende do ICMP)
> length 6: teste + <enter>

---

# ICMP
Utilizado para controlar as atividades de rede.

Controla os protocolos IP, a não ser o TCP, que se autocontrola
Isso, em função do TCP possuir FLAGS e os outros protocolos IP, não.

Existem vários tipos de ICMP, mas a linha básica do protocolo é:
```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Type      |     code      |          checksum             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                             ICMP...                           |

```

## Exemplos de ICMP
* Tipo 8: echo request
* Tipo 8: echo replay
* Tipo 3, código 3: porta de destino inacessível
* Tipo 11, código 0: TTL expirado em trânsito (5, 4, 3, 2, 1, 0)
* Tipo 11, código 1: Tempo de remontagem expirado

**OBS**: Ping possui payload

## Exemplo de captura de ICMP
* 10.1.4.25          == IP do roteador local
* IP 201.22.137.119  == IP do roteador mais próximo
* ICMP 65.54.179.248 == IP do roteador mais distante 
```
21:03:42.745064 IP 201.22.137.119 > 10.1.4.25: ICMP 65.54.179.248 unreachable - 
  need to frag (mtu 1492), length 556
```
> unreachable - need to frag (mtu 1492) == só mtu de tamanho máximo: 1492


## Conectividade
Quando uma máquina consegue enviar um pacote de rede e receber resposta


## PING
Cria um pacote ICMP request e espera um ICMP response

Posui um número de identificação (id) - que não muda,
e um número de sequẽncia - este muda.

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


# MTU
Máxima quantidade de dados que o payload da camada dois (2) Enlace
consegue transmitir

---

# ARP
Protocolo de descoberta de:
- vários tipos de endeçamento de hardware
- vários tipos de endeçamento de protocolo

Serve para descobrir qual o endereço físico,
relacionado com determinado endereço lógico.

Nesse sentido, pode servir para a descoberta
de qual MAC está ligado a qual endereço IP.

## Exemplo de quando ARP é utilizado
O aplicar o comando:
```
  ping 10.0.0.1
```
o ARP vai circular dentro da rede, perguntando:
quem é a máquina cujo IP é **10.0.0.1**

## Exemplo com tcpdump
* -n 				= não resolve nome
* arp       = procura protocolo ARP
```
  sudo tcpdump -n arp
```

### Saída do tcpdump para ARP
* Resquest          = requisição feita por alguma máquina em rede
*  Reply            = resposta a uma requisição (request)
* who-has           = quem é esta máquina
*   tell            = esta máquina pergunta
* is-at             = a máquina requisitada está em <MAC Address>
```
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on enp2s0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
16:10:39.378419 ARP, Request who-has 192.168.0.2 tell 192.168.0.72, length 46
16:10:39.378419 ARP, Request who-has 192.168.0.2 tell 192.168.0.72, length 46
16:10:39.378419 ARP, Request who-has 192.168.0.2 tell 192.168.0.72, length 46
16:10:39.378419 ARP, Request who-has 192.168.0.2 tell 192.168.0.72, length 46
16:10:39.378419 ARP, Request who-has 192.168.0.2 tell 192.168.0.72, length 46
16:10:39.378419 ARP, Request who-has 192.168.0.202 tell 192.168.0.180, length 28
16:10:39.677319 ARP, Reply 192.168.0.202 is-at dc:bf:e9:0f:7f:e3, length 46
```

### Análise da saída do tcpdump
Abaixo, a máquina **192.168.0.72** pergunta, inssistentemente, quem é a máquina **192.168.0.2**.
Isso é um comportamento anômalo, que precisa ser verificado.
```
16:10:39.378419 ARP, Request who-has 192.168.0.2 tell 192.168.0.72, length 46
16:10:39.378419 ARP, Request who-has 192.168.0.2 tell 192.168.0.72, length 46
16:10:39.378419 ARP, Request who-has 192.168.0.2 tell 192.168.0.72, length 46
16:10:39.378419 ARP, Request who-has 192.168.0.2 tell 192.168.0.72, length 46
16:10:39.378419 ARP, Request who-has 192.168.0.2 tell 192.168.0.72, length 46
```

A máquina **192.168.0.180** pergunta, quem é a máquina **192.168.0.202**.
```
16:10:39.378419 ARP, Request who-has 192.168.0.202 tell 192.168.0.180, length 28
```

A máquina **192.168.0.202**, responde que está no siguinte MAC Address: **dc:bf:e9:0f:7f:e3**.
```
16:10:39.677319 ARP, Reply 192.168.0.202 is-at dc:bf:e9:0f:7f:e3, length 46
```

Tendo conseguido este MAC Address, este endereço irá para
uma tabela local e será armazenado dentre: 30s até 30m


## Estrutura do protocolo ARP
      +-----------------------+-----------------------+
      |     0     |     1     |     2     |     3     |
      +-----------------------+-----------------------+
   0  | Hardware Address Type | Protocol Address Type |
      +-----------------------+-----------------------+
      | Hardware  | Protocol  |                       |
   4  |  Address  |  Address  |        OPCODE         |
      |  length   |  length   |                       |
      +-----------------------+-----------------------+
   8  |            Source Hardware Address            |
      +-----------------------+-----------------------+
  12  |Source Hardware Address|Source Protocol Address|
      +-----------------------+-----------------------+
  16  |Source Hardware Address|Target Hardware Address|
      +-----------------------+-----------------------+
  20  |        Target Hardware Address (cont.)        |
      +-----------------------+-----------------------+
  24  |        Target Protocol Address (cont.)        |
      +-----------------------+-----------------------+

---

# TEST-NET-1
> Para documentação: RFC C5737
```
  192.0.2.0/24
```

# TEST-NET-2
> Para documentação: RFC C5737
```
  198.51.100.0/24
```

# TEST-NET-3
> Para documentação: RFC C5737
```
  203.0.113.0/24
```

# TEST-NET IPv6
> Para documentação: RFC 3849
```
  2001:db8::/32
```

---

# MODELO OSI: ESTRUTURA
```
  camada 2  header Ethernet
  camada 2  payload Ethernet { 

  camada 3    header  IP
  camada 3    payload IP { 

  camada 4      header TCP
  camada 4      payload TCP {

  camada 7        http

  camada 4      }
  camada 3    }
  camada 2  }
```

## Exemplo utilizando http
```
+--------------+  +-------------------------+                      +------+
|   Aplicação  |  |      Encapsulamento     |                      | HTTP |
+--------------+  +-------------------------+                      +------+
| Apresentação |  |        Preparação       |                          |
+--------------+  +-------------------------+                          |
|    Sessão    |  |         Controle        |                          |
+--------------+  +-------------------------+                    +--------------------+
|  Transporte  |  | Encapsulamento/Controle |                    | |header|    TCP    |
+--------------+  +-------------------------+           +--------+--------------------+
|     Rede     |  | Encapsulamento/Controle |           | |header|        IP(v4 e v6) | 
+--------------+  +-------------------------+   +--------+----------------------------+
|    Enlace    |  | Encapsulamento/Controle |   | |header|                  Ethernet  |
+--------------+  +-------------------------+   +-------------------------------------+
|    Física    |  |         Despacho        |
+--------------+  +-------------------------+

```
> Sem usuário, não há necessidade de usar as camadas: 4, 5, 6, 7

## MODELO OSI: APRESENTAÇÂO
Formata para a sessão de Aplicação
Criptografia (SSl), conversão de padrões, (des)compressão (gzip)

## MODELO OSI: SESSÂO
Realiza o reconhecimento de canal entre as partes comunicantes
Um SSH, FTP ou Telnet pedindo senha para continuar trocando informações.

---

# Técnicas de uso para análise de tráfego
Caso 1:
  bloqueio do tráfego em um elemento intermediário de rede
  (CLIENT não consegue comunicar SERVER)
  (regra de filtragem mal feitas, erro no roteador etc.)
```
   ___         ____         ____          ___ 
  /   |       |    |       |    |        /   | 
 /    | ----- |    | ----- |    | ----- /    | 
|_____|       |____|       |____|      |_____| 
CLIENT       ROTEADOR     ROTEADOR      SERVER
                1             2
```

  Aplicar tcpdump ao longo da topologia para descobrir
  o ponto de bloqueio

```
       SYN SYN      SYN SYN      SYN NADA --- erro foi aqui
   ___  /   \  ____  /   \  ____  /    \  ___ 
  /   |/     \|    |/     \|    |/      \/   | 
 /    | ----- |    | ----- |    | ----- /    | 
|_____|       |____|       |____|      |_____| 
CLIENT       ROTEADOR     ROTEADOR      SERVER
                1             2
```



Caso 2:
  bloqueio do tráfego por falha física na topologia

```
   ___         ____         ____          ___ 
  /   |       |    |       |    |        /   | 
 /    | ----- |    | ----- |    | ----- /    | 
|_____|       |____|       |____|      |_____| 
CLIENT       ROTEADOR     ROTEADOR      SERVER
                1             2
```

  Aplicar tcpdump ao longo da topologia para descobrir
  o ponto de bloqueio
                                       
```
                     ┌───────── erro foi aqui: saiu um SYN, mas não chegou na outra máquina
       SYN SYN      SYN NADA 
   ___  /   \  ____  /   \  ____          ___ 
  /   |/     \|    |/     \|    |        /   | 
 /    | ----- |    | ----- |    | ----- /    | 
|_____|       |____|       |____|      |_____| 
CLIENT       ROTEADOR     ROTEADOR      SERVER
                1             2
```

Caso 3:
  Falha de conexão em serviços
  Uso do tcpdump numa arquitetura CLIENT-SERVER (camada de Aplicação, 7)

```
   ____         ______ 
  /    |       |      | 
 /     | ----- |      | 
|______|       |______| 
 CLIENT         SERVER
```

  Aplicar tcpdump com -A, para olhar o payload

* 192.168.1.104.3306  == MySQL Server (geralmente, MySQL roda na porata 3306)
* 192.168.1.101.34941 == CLIENT
```
00:12:03.499715 IP 192.168.1.104.3306 > 192.168.1.101.34941: Flags[P.], seq 1:75, 
  ack 1, win 33, options [nop,nop,TS val 23718975 ecr 5218436], length 74
E..~..@.@......h...e...}.(..@1&....!.......
.i.?.0..F....j.Host '192.168.1.101' is not allowed to connect to this MySQL server
```
> CLIENT não possui permissão para realizar conexão ao SERVER


Caso 4:
  Falha de conexão em serviços
  Uso do tcpdump numa arquitetura CLIENT-SERVER (camada de Aplicação, 7)

```
   ____         ______ 
  /    |       |      | 
 /     | ----- |      | 
|______|       |______| 
 CLIENT         SERVER
```

  Aplicar tcpdump com -A, para olhar o payload

* 172.16.10.49.3306   == MySQL Server (geralmente, MySQL roda na porata 3306)
* 172.16.10.42.39903  == CLIENT
```
00:12:03.499715 IP 172.16.10.49.3306 > 172.16.10.42.39903: Flags[P.], seq 79:162, 
  ack 80, win 101, options [nop,nop,TS val 3773032 ecr 3202030], length 83
E....E@.@......1...*......bx........Z......
.9.h.0..0......#42000Acess denied for usar 'alpha31'@'172.16.10.42' to database 
  'wikinet3'
```
> CLIENT possui acesso ao SERVER, mas não ao database selecionado

---

# LINKS EXTRAS
  
## Conceitos básicos do protocolo HTTP:
  HTTP Tutorial                       
      -> https://www.tutorialspoint.com/http/index.htm
 
## Mensagens HTTP:
   HTTP Headers for Dummies            
       -> https://code.tutsplus.com/tutorials/http-headers-for-dummies--net-8039
 
## Cabeçalhos HTTP:
   HTTP (HyperText Transfer Protocol)  
       -> https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/HTTP_Basics.html
   
## Animação do Protocolo de Janela Deslizante:
   protocolos de janela deslizante 'go back n' e 'selective repeat'.
       -> http://www.ccs-labs.org/teaching/rn/animations/gbn_sr/
