# DNAT
Serviço funcionando numa máquina virtual,
da sua máquina real
possa ser acessado por uma máquina real, que esteja na rede local  

---

# Permission
Libera máquina real, para realizar encaminhamento de IP  
```
    echo "1" > /proc/sys/net/ipv4/ip_forward
```  

* -I <NEW_RULE> = inclua uma nova regra. No caso, dentro da chain chamada FORWARD.  
* -m <PROPERTY> = procura uma PROPRIEDADE específica. No caso, a propriedade chamada "state".  
* -d <IP_GATEWAY> = definição do IP de destino desta nova regra. No caso, IP_GATEWAY  
* --state <STATEMENT> = permissões do estado ao acessar estas condições.  
* -j <TARGET_OF_THE_RULE> = definição do local (o que fazer) que haverá o redirecionamento (caso a regra combine). No caso, ACCEPT  

## Example Redirect: generic
```
    iptables -I <NEW_RULE> -m <PROPERTY> -d <IP_GATEWAY> --state NEW,RELATED,ESTABLISHED -j ACCEPT
```  

## Example Redirect: with configs
```
    iptables -I FORWARD -m state -d 192.168.100.0/24 --state NEW,RELATED,ESTABLISHED -j ACCEPT
```  

---

* -t <TABLE> = atue sobre a tabela. No caso, nat.  
* -I <NEW_RULE> = inclua uma nova regra. No caso, dentro da chain chamada PREROUTING.  
* -p <PROTOCOLO> = escolha o protocolo. No caso, tcp.  
* -d <IP_MACHINE> = definição do IP de destino desta nova regra. No caso, IP da máquina local  
* --dport <PORT_MACHINE> = definição da porta. No caso, porta 80.  
* -j <TARGET_OF_THE_RULE> = definição do local (o que fazer) que haverá o redirecionamento (caso a regra combine). No caso, DNAT  
* --to-destination i<IP_VIRTUAL_MACHINE>:<PORT> =  para onde será redirecionamento. No caso, ip da máquina virtual e porta da máquina virtual  

## Example Redirect: generic
```
    iptables -t <TABLE> -I <NEW_RULE> -p <PROTOCOLO> -d <IP_MACHINE> --dport <PORT_MACHINE> -j <TARGET_OF_THE_RULE> --to-destination <IP_VIRTUAL_MACHINE>:<PORT>
```  

## Example Redirect: with configs
```
    iptables -t nat -I PREROUTING -p tcp -d 192.168.15.53 --dport 80 -j DNAT --to-destination 192.168.100.2:80
```  
