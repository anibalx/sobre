# Sockets
são abstrações das camadas de rede para aplicações 
que precisam se comunicar com outras aplicações através de redes.

**OBS**
> Durante uma conexção, sockets do Client-Server NUNCA MUDAM \
  Caso aconteça de mudar, já é caracterizado como OUTRA conexão


Basicamente é a combinação de
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

# Lista sockets (TYPE, PORT, INODE, UID, PID, FD, NAME)
```
  socklist
```

# ss
Lista os sockets abertos no sistema
* -o = options
```
  ss -o state established '( sport = :http or sport = :https )'
```
* -t  = mostra para TCP
* -n  = não resolva o DNS
* src = seta a porta de origem, pode ser 80 ou 443
```
  ss -tn src :<PORT> or src :<PORT>
  ss -tn src :80 or src :443
```

## Fuser
Identifique processos usando arquivos ou sockets
```
  fuser 443/tcp
  fuser 68/udp
```


sockets, tomadas
são abstrações das camadas de rede para aplicações 
que precisam se comunicar com outras aplicações através de redes.

Basicamente é a combinação de
protocolo + IP + porta.

EX:
    PROTOCOLO://IP:PORTA
        http://1.1.1.1:80

# REFERÊNCIAS
https://blog.pantuza.com/artigos/o-que-sao-e-como-funcionam-os-sockets
https://www.ateomomento.com.br/sockets/
