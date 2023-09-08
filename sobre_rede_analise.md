# Exemplo de verificação e adição de rede

## Contexto
Ao tentar acessar um SERVER, através do protocolo ssh
a conexão não estava sendo realizada.


## Dados Iniciais
IPv4 do CLIENT
- **10.0.0.105/24**

IPv4 do SERVER
- **10.0.0.250/24**


## Buscas para solucionar o problema 

### Primeira parte
Dentro do SERVER verificou-se o log com:
* -f || --follow == cauda do log
```
  journalctl -f
```

Análise da máquina CLIENT em busca do contexto
```
  ip r
```

Saída de `ip r` dentro da máquina CLIENT
* default via <IP> = para que máquina dentro da rede os pacotes serão enviados  
* <IP>/CIDR = rede na qual esta máquina esta inserida  
* src <IP>  = própria máquina (ou servidor DHCP)
```
  default via 10.0.0.2 dev wlo1 proto dhcp metric 600 
  10.0.0.0/24 dev wlo1 proto kernel scope link src 10.0.0.105 metric 600
```

Note a segunda linha da saída do comando `ip r`.
- 10.0.0.0/24 dev wlo1 proto kernel scope link src 10.0.0.105 metric 600

Tudo que está compreendido dentro do segmento de rede
- **10.0.0.0/24** 
Está sendo direcionado para a própria máquina CLIENT
- **10.0.0.105** 


#### Explicação dos processos
Ao "subir" uma interface de rede, 3 rotas são estabelecidas
- rota para a rede: **10.0.0.0/24**
- rota default: **10.0.0.2**
- rota para a própria máquina: **10.0.0.105**

Dentro do contexto do problema, todo tráfego do segmento de rede
- **10.0.0.0/24** 
estava sendo direcionado para a máquina CLIENT 
- **10.0.0.105**
O que não deveria acontecer.


#### Resolução do problema

* del == deleta rota (aqui, rota para a rede)
```
  ip route 10.0.0.0/24
```

### Segunda parte

A partir de CLIENT, verificação de estado de SERVER
```
  nmap -n -p 22 10.0.0.250
```

Saída do nmap
```
  PORT      STATE       SERVICE
  22/tcp    open        ssh
```
o SERVER está presente no mesmo segmento de rede que o CLIENT

A partir de CLIENT, acesso via __ssh__ ao SERVER
```
  ssh fe80::7a2b::cbff::fe8d::f3b2%wlo1
```
A conexão foi realizada, mas apenas usando IPv6.


Ainda dentro do SERVER verificou-se o log com:
* -f || --follow == cauda do log
```
  journalctl -f
```
Como não apresentava nada, deduziu-se que a conexão não estava sendo estabelecida.


Em uma outra máquina e mesmo segmento de rede, 
utilizou-se um ping até o SERVER para testar a conexão:
```
  ping 10.0.0.250
```
Esta outra máquina recebeu um "pong" e a resposta apareceu dentro do "journalctl" do SERVER.
Isso indicou, que o problema de conexão estava na primeira máquina.


Em busca de resolver o problema, um programa de interface começada por "zcc", 
foi encerrado e isso, desabilitou a configuração padrão da interface de rede.
Que não retornou ao padrão.
A rota de rede teria um número como:
```
  10.0.0.0/24
```
Essa rota foi desabilitada na primeira parte da resolução do problema.
Ao usar o comando `ip r`, a rota da própria rede **10.0.0.0/24**, não foi exibida
```
  ip r
```
Saída do ip r
* default via <IP> = para que máquina dentro da rede os pacotes serão enviados  
```
  default via 10.0.0.2 dev wlo1 proto dhcp metric 600 
```

#### Explicação dos processos
Ao "subir" uma interface de rede, 2 rotas são estabelecidas
- rota para a rede: **10.0.0.0/24**
- rota default: **10.0.0.2**

Dentro do contexto do problema, como não há uma rota **10.0.0.0/24**
para as máquinas dentro desta rede, a infraestrutura envia 
para o roteador default **10.0.0.2**


#### Resolução do problema

* add == adiciona nova rota (aqui, rota padrão)
```
  ip route add 10.0.0.0/24 dev wlo1
```

* default via <IP> = para que máquina dentro da rede os pacotes serão enviados  
* <IP>/CIDR = rede na qual esta máquina esta inserida  
```
  default via 10.0.0.2 dev wlo1 proto dhcp metric 600 
  10.0.0.0/24 dev wlo1 scope link
```

#### Teste da Resolução do Problema
```
  traceroute 10.0.0.250
```
