# Antigo Comando x Novo Comando
ifconfig -a                                                 | ip a
ifconfig enp6s0 down                                        | ip link set enp6s0 down
ifconfig enp6s0 up                                          | ip link set enp6s0 up
ifconfig enp6s0 192.168.2.24                                | ip addr add 192.168.2.24/24 dev enp6s0
ifconfig enp6s0 netmask 255.255.255.0                       | ip addr add 192.168.1.1/24 dev enp6s0
ifconfig enp6s0 mtu 9000                                    | ip link set enp6s0 mtu 9000
ifconfig enp6s0:0 192.168.2.25                              | ip addr add 192.168.2.25/24 dev enp6s0
netstat                                                     | ss
netstat -tulpn                                              | ss -tulpn
netstat -neopa                                              | ss -neopa
netstat -g                                                  | ip maddr
route                                                       | ip r
route add -net 192.168.2.0 netmask 255.255.255.0 dev enp6s0 | ip route add 192.168.2.0/24 dev enp6s0
route add default gw 192.168.2.254                          | ip route add default via 192.168.2.254
arp -a                                                      | ip neigh
arp -v                                                      | ip -s neigh
arp -s 192.168.2.33 1:2:3:4:5:6                             | ip neigh add 192.168.3.33 lladdr 1:2:3:4:5:6 dev enp6s0
arp -i enp6s0 -d 192.168.2.254                              | ip neigh del 192.168.2.254 dev wlp7s0

# Objetos
objetos   | Forma Abreviada | Propósito
link      |        l        | Dispositivo de rede
address   |    a, addr      | Endereço de Protocolo (IPv4 ou IPv6) num dispositivo
addrlabel |      addrl      | Configuração de label (rótulo) para a seleção de endereço de protocolo
neighbour |    n, neigh     | ARP ou NDISC
route     |        r        | Entrada de tabela de roteamento
rule      |       ru        | Regra em política de roteamento de database
maddress  |    m, maddr     | Endereço Multicast
mroute    |       mr        | Entrada de chace de roteamento multicast
tunnel    |        t        | Túnel sobre IP
xfrm      |        x        | Framework para protocol IPsec

# Exibição curta
```
ip -br a
ip -brief a
```  

# IPv4
```
ip -4 a
```  

# IPv6
```
ip -6 a
```  

# Exiba UMA interface específica
```
ip a list enp0s2
ip a show enp0s2
```  

# Conexões ativas
```
ip link ls up
```  

# Cache arp e neighbour (vazio)
```
ip neigh
ip n show
ip neighbour show
ip neighbour show dev <INTERFACE>
```  

* Stale: Significa que o vizinho (neighbour) é válido mas é provavelmente “Não alcançável”. O kernel irá tentar checar ele na primeira retransmissão
* Delay: Um pacote foi enviado para o vizinho (neighbour) e o kernel está esperando para confirmar
* Reachable: o vizinho (neighbour) é válido e aparentemente alcançável.


# Adicionando uma nova entrada arp
```
ip neigh add {IP-AQUI} lladdr {MAC/LLADDRESS} dev {DISPOSITIVO} nud {Estado}
```  

"**nud**" pode receber os seguintes valores(estados):  

* permanent: a entrada criada será permanente só poderá ser excluída com intervenção do usuário administrador.
* noarp: A entrada é válida. Nenhuma tentativa para validar essa entrada será feita mas ela será removida quando expirar o seu tempo.
* stale: a entrada é válida, mas suspeita.
* reachable: essa entrada é válida até o tempo de vida(lifetime) expirar
```
sudo ip n add 10.1.1.32 lladdr 08:00:27:9a:13:eb dev enp0s8 nud perm
```  

> perm == permanente


## Delete a entrada arp
```
sudo ip n del 10.1.1.32 dev enp0s8
```  

# Tabela de Roteamento
```
ip r
ip r list
ip route list
ip r list [options] ip route
```  

## Adição de uma nova rota
```
ip route add {NETWORK/MASK} via {GATEWAYIP}
ip route add {NETWORK/MASK} dev {DEVICE}
```  

## Adiciona uma rota padrão usando ip
```
ip route add default {NETWORK/MASK} dev {DEVICE}
ip route add default {NETWORK/MASK} via {GATEWAYIP}
```  

### Adição de rota: Exemplo
```
ip route add 192.168.1.0/24 via 192.168.1.254
ip route add 192.168.1.0/24 dev eth0
```  

### Deleção de rota
```
ip route del default
ip route del 192.168.1.0/24 dev eth0
```  

---

# Ip
A sintaxe é: ip a add {endereço/máscara} dev {interface}

**Obs**
As atribuições e remoção de IPs abaixo são temporários,
pois o que permanece é a configuração dentro de /etc/network/interfaces. 

Após reiniciar os ips adicionados com “ip a add” ou removidos com “ip a del” são perdidas.

## Adição de ip
```
sudo ip a add 10.0.0.100/24 dev enp0s8
```  

## Remoção de ip
```
sudo ip a del 10.1.1.31 dev enp0s8
sudo ip a flush dev enp0s8 # remove tudo ligado a interface "enp0s8"
```  

---

# Dispositivos de Rede
## Desativa
```
sudo ip link set enp0s8 down
```  

## Ativa
```
sudo ip link set enp0s8 up
```  

---

# TXQUEUELEN
txqueuelen:

* tx: taxa
* queue: fila
* len: quantidade. len vem de length.

Podemos mudar o tamanho da transmit queue (fila de transmissão) usando: 
```
ip link set txqueuelen {NUMBER} dev {DEVICE}
```  

## Alterando o txqueuelen do dispositivo enp0s8
```
sudo ip link set txqueuelen 1000 dev enp0s8
```  

## Vamos colocar o txqueuelen para 10000
```
sudo ip link set txqueuelen 10000 dev enp0s8
```  

---

# MTU
A sintaxe para alterar a mtu ou unidade máxima de transmissão é:  

## Exemplo: mtu
```
ip link set mtu {NUMBER} dev {DEVICE}
```  

```
sudo ip link set mtu 9000 dev enp0s8
```  

---

# MAC
Alteração do endereço atual do dispositivo  
Vamos alterar de **08:00:27:e0:30:88** para **99:99:99:e0:30:88**  

## Desative a placa
```
sudo ip link set dev enp0s8 down
```  

## Altere o endereço da placa
```
sudo ip link set dev enp0s8 address 99:99:99:e0:30:88
```  

## Reative a placa
```
sudo ip link set dev enp0s8 up
```  

---

# REFERÊNCIAS
[Gnu Linux Brasil - linux usando o comando ip](https://www.gnulinuxbrasil.com.br/2021/03/02/linux-usando-o-comando-ip/)
[B[oson Treinametos - linux usando o comando ip](http://www.bosontreinamentos.com.br/linux/10-exemplos-de-configuracao-de-rede-com-comandos-ip-no-linux/)
