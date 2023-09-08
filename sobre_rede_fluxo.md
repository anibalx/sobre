# Exemplo IP

## NetCat
Em um terminal (tty) - ou emulador de terminal (pts), ou aba etc.  
 * -l == lista a porta  
```
  nc -l 1234
```

Em outro terminal (tty) - ou emulador de terminal (pts), ou aba etc.  
```
  nc 127.0.0.1 1234
```

## TCPDUMP
Em outro terminal (tty) - ou emulador de terminal (pts), ou aba etc.
* -tttt    == ano, mês, dias, hora, minuto, segundos e frações de segundos
* -nnn     == não resolva nome e limpe a exibição
* -i       == interface de rede: loopback
* port or  == as portas que devem estar a escuta
```
  sudo tcpdump -ttttnnni lo port 80 or port 81 or port 1234
```

**OBS**
> No caso de um download muito grande, o P (de Push) pode ser omitido
  e um ponto (.) similar ao ACK, colocado na exibição do tcpdump


### Exemplo de captura através do tcpdump
```
  tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
  listening on lo, link-type EN10MB (Ethernet), snapshot length 262144 bytes

  2022-05-06 11:04:31.102796 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [S], seq 810775634, win 65495, options [mss 65495,sackOK,TS val 2518909665 ecr 0,nop,wscale 7], length 0
  2022-05-06 11:04:31.102830 IP 127.0.0.1.1234 > 127.0.0.1.44980: Flags [S.], seq 1555075220, ack 810775635, win 65483, options [mss 65495,sackOK,TS val 2518909665 ecr 2518909665,nop,wscale 7], length 0
  2022-05-06 11:04:31.102855 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [.], ack 1, win 512, options [nop,nop,TS val 2518909665 ecr 2518909665], length 0
  2022-05-06 11:05:25.591261 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [P.], seq 1:6, ack 1, win 512, options [nop,nop,TS val 2518964153 ecr 2518909665], length 5
  2022-05-06 11:05:25.591296 IP 127.0.0.1.1234 > 127.0.0.1.44980: Flags [.], ack 6, win 512, options [nop,nop,TS val 2518964153 ecr 2518964153], length 0
  2022-05-06 11:06:13.471542 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [F.], seq 6, ack 1, win 512, options [nop,nop,TS val 2519012034 ecr 2518964153], length 0
  2022-05-06 11:06:13.471600 IP 127.0.0.1.1234 > 127.0.0.1.44980: Flags [F.], seq 1, ack 7, win 512, options [nop,nop,TS val 2519012034 ecr 2519012034], length 0
  2022-05-06 11:06:13.471627 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [.], ack 2, win 512, options [nop,nop,TS val 2519012034 ecr 2519012034], length 0
```


#### Conexão entre Client e Server
```
  2022-05-06 11:04:31.102796 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [S], seq 810775634, win 65495, options [mss 65495,sackOK,TS val 2518909665 ecr 0,nop,wscale 7], length 0
  2022-05-06 11:04:31.102830 IP 127.0.0.1.1234 > 127.0.0.1.44980: Flags [S.], seq 1555075220, ack 810775635, win 65483, options [mss 65495,sackOK,TS val 2518909665 ecr 2518909665,nop,wscale 7], length 0
  2022-05-06 11:04:31.102855 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [.], ack 1, win 512, options [nop,nop,TS val 2518909665 ecr 2518909665], length 0
```


#### Envio de um Push (PSH) do Client e resposta do Server
```
  2022-05-06 11:05:25.591261 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [P.], seq 1:6, ack 1, win 512, options [nop,nop,TS val 2518964153 ecr 2518909665], length 5
  2022-05-06 11:05:25.591296 IP 127.0.0.1.1234 > 127.0.0.1.44980: Flags [.], ack 6, win 512, options [nop,nop,TS val 2518964153 ecr 2518964153], length 0
```

#### Encerramento de conexão entre o Client e o Server
```
  2022-05-06 11:06:13.471542 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [F.], seq 6, ack 1, win 512, options [nop,nop,TS val 2519012034 ecr 2518964153], length 0
  2022-05-06 11:06:13.471600 IP 127.0.0.1.1234 > 127.0.0.1.44980: Flags [F.], seq 1, ack 7, win 512, options [nop,nop,TS val 2519012034 ecr 2519012034], length 0
  2022-05-06 11:06:13.471627 IP 127.0.0.1.44980 > 127.0.0.1.1234: Flags [.], ack 2, win 512, options [nop,nop,TS val 2519012034 ecr 2519012034], length 0
```

### Encerramento do TCPDUMP
```
  8 packets captured
  16 packets received by filter
  0 packets dropped by kernel
```

### Detalhamento de linha do tcpdump
> Solicitação de conexão do Client ao Server
* 2022-05-06             == ano, mês e ano
* 11:04:31.102796        == hora, minuto, segundo,frações de segundos
* IP 127.0.0.1.44980     == IP Client, numa porta aleatória
* >                      == mostra o fluxo de envio do IP
* 127.0.0.1.1234         == IP Server, na porta estabelecido no nc 
* :                      == separação de informações, aqui protocolo IP
* Flags [S]              == flag (SYN) enviada do Client ao Server, para estabelecer a conexão
* seq 810775634          == número de sequência
* win 65495              == reserva de buffer, em geral, começa com número baixo e vai crescendo até estabilizar
* options [...]          == seta as opções para utilizar com os protocolos IP
  1. options [..., wscale7] == potencializa janela de bytes para as próximas janelas que NÂO sâo SYN: win <NUM> ^ 7
* length 0               == tamanho do payload, como não existe payload, o tamanho é zero


> Resposta do Server ao Client
* 2022-05-06             == ano, mês e ano
* 11:04:31.102830        == hora, minuto, segundo,frações de segundos
* 127.0.0.1.1234         == IP Server, na porta estabelecido no nc 
* >                      == mostra o fluxo de envio do IP
* IP 127.0.0.1.44980     == IP Client, numa porta aleatória
* :                      == separação de informações, aqui protocolo IP
* Flags [S.]             == flags [S.] SYN e ACK enviadas do Server ao Client, confirmando o recebimento do SYN
* seq 1555075220         == número de sequência
* ack 810775635          == confirmação de que é conhecido o número de sequência do próximo segmento a ser enviado pelo Server
* win 65483              == reserva de buffer, em geral, começa com número baixo e vai crescendo até estabilizar
* options [...]          == seta as opções para utilizar com os protocolos IP
  1. options [..., wscale7] == potencializa janela de bytes para as próximas janelas que NÂO sâo SYN: win <NUM> ^ 7
* length 0               == tamanho do payload, como não existe payload, o tamanho é zero


> Resposta do Client ao Server
* 2022-05-06             == ano, mês e ano
* 11:04:31.102855        == hora, minuto, segundo,frações de segundos
* IP 127.0.0.1.44980     == IP Client, numa porta aleatória
* >                      == mostra o fluxo de envio do IP
* 127.0.0.1.1234         == IP Server, na porta estabelecido no nc 
* :                      == separação de informações, aqui protocolo IP
* Flags [.]              == flags [.] ACK enviadas do Client ao Server, confirmando o recebimento do SYN
* seq 1555075220         == número de sequência
* ack 1                  == confirmação de que é conhecido o número de sequência do próximo segmento a ser enviado pelo Client
* win 512                == reserva de buffer, em geral, começa com número baixo e vai crescendo até estabilizar
* options [...]          == seta as opções para utilizar com os protocolos IP
  1. options [..., wscale7] == potencializa janela de bytes para as próximas janelas que NÂO sâo SYN: win <NUM> ^ 7
* length 0               == tamanho do payload, como não existe payload, o tamanho é zero


> Envio de payload (PSH) do Client ao Server
* 2022-05-06             == ano, mês e ano
* 11:05:25.591261        == hora, minuto, segundo,frações de segundos
* IP 127.0.0.1.44980     == IP Client, numa porta aleatória
* >                      == mostra o fluxo de envio do IP
* 127.0.0.1.1234         == IP Server, na porta estabelecido no nc 
* :                      == separação de informações, aqui protocolo IP
* Flags [P.]             == flags [P.] PSH e ACK enviadas do Client ao Server
* seq 1:6                == intervalo (número) de sequência do payload enviado: 1push<enter>
* ack 1                  == confirmação de que é conhecido o número de sequência do próximo segmento a ser enviado pelo Client
* win 512                == win 512 ^ 7, reserva de buffer, 512 elevado a 7, como demonstrado em options[..., wscale7]
* options [...]          == seta as opções para utilizar com os protocolos IP
* length 5               == tamanho do payload: push<enter>


> Resposta do Server ao payload (PSH) do Client
* 2022-05-06             == ano, mês e ano
* 11:05:25.591296        == hora, minuto, segundo,frações de segundos
* 127.0.0.1.1234         == IP Server, na porta estabelecido no nc 
* >                      == mostra o fluxo de envio do IP
* IP 127.0.0.1.44980     == IP Client, numa porta aleatória
* :                      == separação de informações, aqui protocolo IP
* Flags [.]              == flags [.] ACK enviadas do Server ao Client
* ack 6                  == confirmação de que é conhecido o número de sequência do próximo segmento a ser enviado pelo Client
* win 512                == win 512 ^ 7, reserva de buffer, 512 elevado a 7, como demonstrado em options[..., wscale7]
* options [...]          == seta as opções para utilizar com os protocolos IP
* length 0               == tamanho do payload, como não existe payload, o tamanho é zero


> Solicitação de encerramento de conexão do Client ao Server 
* 2022-05-06             == ano, mês e ano
* 11:06:13.471542        == hora, minuto, segundo,frações de segundos
* IP 127.0.0.1.44980     == IP Client, numa porta aleatória
* >                      == mostra o fluxo de envio do IP
* 127.0.0.1.1234         == IP Server, na porta estabelecido no nc 
* :                      == separação de informações, aqui protocolo IP
* Flags [F.]             == flags [F.] FYN e ACK enviadas do Client ao Server, para solicitar encerramento de conexão
* seq 6                  == número de sequência
* ack 1                  == confirmação de que é conhecido o número de sequência do próximo segmento a ser enviado pelo Client
* win 512                == win 512 ^ 7, reserva de buffer, 512 elevado a 7, como demonstrado em options[..., wscale7]
* options [...]          == seta as opções para utilizar com os protocolos IP
* length 0               == tamanho do payload, como não existe payload, o tamanho é zero

> Resposta do Server a solicitação de encerramento de conexão do Client
* 2022-05-06             == ano, mês e ano
* 11:06:13.471600        == hora, minuto, segundo,frações de segundos
* 127.0.0.1.1234         == IP Server, na porta estabelecido no nc 
* >                      == mostra o fluxo de envio do IP
* IP 127.0.0.1.44980     == IP Client, numa porta aleatória
* :                      == separação de informações, aqui protocolo IP
* Flags [F.]             == flags [F.] FYN e ACK enviadas do Server ao Client , em resposta a solicitação de conexão
* seq 1                  == número de sequência
* ack 7                  == confirmação de que é conhecido o número de sequência do próximo segmento a ser enviado pelo Client
* win 512                == win 512 ^ 7, reserva de buffer, 512 elevado a 7, como demonstrado em options[..., wscale7]
* options [...]          == seta as opções para utilizar com os protocolos IP
* length 0               == tamanho do payload, como não existe payload, o tamanho é zero


> Resposta do Client ao encerramento de conexão do Server
* 2022-05-06             == ano, mês e ano
* 11:06:13.471627        == hora, minuto, segundo,frações de segundos
* IP 127.0.0.1.44980     == IP Client, numa porta aleatória
* >                      == mostra o fluxo de envio do IP
* 127.0.0.1.1234         == IP Server, na porta estabelecido no nc 
* :                      == separação de informações, aqui protocolo IP
* Flags [.]              == flags [.] ACK enviadas do Client ao Server, em resposta a solicitação de conexão
* ack 2                  == confirmação de que é conhecido o número de sequência do próximo segmento a ser enviado ao Server
* win 512                == win 512 ^ 7, reserva de buffer, 512 elevado a 7, como demonstrado em options[..., wscale7]
* options [...]          == seta as opções para utilizar com os protocolos IP
* length 0               == tamanho do payload, como não existe payload, o tamanho é zero


---


# Exemplo TCP

## IPTABLES
IPTABLES, bloqueie tudo que vier para a porta 81 desta máquina
* -A || --append   INPUT == esta máquina
* -p || --protocol tcp   == protocolo
* --dport                == porta
* -j || --jump     DROP  == descarte
```
  iptables -A INPUT -p tcp --dport 81 -j DROP
```

## TCPDUMP
Em um terminal (tty) - ou emulador de terminal (pts), ou aba etc.
* -tttt    == ano, mês, dias, hora, minuto, segundos e frações de segundos
* -nnn     == não resolva nome e limpe a exibição
* -i       == interface de rede: loopback
* port or  == as portas que devem estar a escuta
* -v       == mostra informações sobre o IP
```
  sudo tcpdump -ttttnnni lo port 81
```

## Telnet
Em outro terminal (tty) - ou emulador de terminal (pts), ou aba etc.
```
  telnet 127.0.0.5 81
```
> ao passar um número de uma porta que não existe, SERVER retorna um RST (Reset == "não entendi")


### Exemplo de captura através do tcpdump (Bloqueio de Porta)
TCP possui o mesmo número de sequência, indicando que é o mesmo seguimento TCP
Contudo, o id do IP muda.
Então, IP (caminhão) muda, mas o TCP (carga) deve ser similiar, identica até a resposta ser obtida.

Além disso, note como o tempo de reetransmissão (em segundos) muda.
O tempo dobra em relação ao anterior (reetransmissão rápida).
```
  tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
  listening on lo, link-type EN10MB (Ethernet), snapshot length 262144 bytes

  2022-05-06 11:04:31.102796 IP (tos 0x10, ttl 64, id 40256, offset 0, flags [DF], proto TCP (6), length 60)
    127.0.0.1.50688 > 127.0.0.5.81: Flags [S], cksum 0xfe34 (incorrect -> 0xd8bb), seq 810775634, win 65495, 
  options [mss 65495,sackOK,TS val 2518909665 ecr 0,nop,wscale 7], length 0

  2022-05-06 11:04:32.102686 IP (tos 0x10, ttl 64, id 40257, offset 0, flags [DF], proto TCP (6), length 60)
    127.0.0.1.50688 > 127.0.0.5.81: Flags [S], cksum 0xfe34 (incorrect -> 0xd4cd), seq 810775634, win 65495, 
  options [mss 65495,sackOK,TS val 2518989874 ecr 0,nop,wscale 7], length 0

  2022-05-06 11:04:34.103783 IP (tos 0x10, ttl 64, id 40258, offset 0, flags [DF], proto TCP (6), length 60)
    127.0.0.1.50688 > 127.0.0.5.81: Flags [S], cksum 0xfe34 (incorrect -> 0xcced), seq 810775634, win 65495, 
  options [mss 65495,sackOK,TS val 2519456429 ecr 0,nop,wscale 7], length 0
```

> **OBS**: novamente, este é um exemplo de reetransmissão rápida

### Detalhamento de linha do tcpdump
> Solicitação de conexão do Client ao Server
* 2022-05-06                                     == ano, mês e ano
* 11:04:31.102796                                == hora, minuto, segundo, frações de segundos
* IP (...)                                       == informações sobre o IP
  1. IP (tos 0x10, ...)                          == type of service
  2. IP (..., ttl 64, ...)                       == time to live
  3. IP (..., id 40256, ...)                     == número de identificação (acknowledgment number) do IP
  4. IP (..., offset 0, ...)                     == data offset
  5. IP (..., flags [DF], ...)                   == flags TCP
  6. IP (..., proto TCP (6), ...)                == tipo de protocolo que IP carrega
  7. IP (..., length 60)                         == tamanho do IP
* 127.0.0.1.50688                                == IP Client, numa porta aleatória (socket de origem)
* >                                              == mostra o fluxo de envio do IP
* 127.0.0.1.81                                   == IP Server, na porta estabelecido no nc 
* :                                              == separação de informações, aqui protocolo IP
* Flags [S]                                      == flag (SYN) enviada do Client ao Server, para estabelecer a conexão
* cksum 0xfe34 (incorrect -> 0xd8bb)             == cksum TCP
* seq 810775634                                  == número de sequência
* win 65495                                      == reserva de buffer, em geral, começa com número baixo e vai crescendo até estabilizar
* options [...]                                  == seta as opções para utilizar com os protocolos IP
  1. options [..., TS val 2518909665 ecr 0, ...] == Time Stamp: valor decorrido desde algum ponto (depende do OS) | Echo Reply: time stamp enviado e retornado, só que do lado do SERVER
  2. options [..., wscale7]                      == potencializa janela de bytes para as próximas janelas que NÂO sâo SYN: win <NUM> ^ 7
* length 0                                       == tamanho do payload, como não existe payload, o tamanho é zero


> Solicitação de conexão do Client ao Server
* 2022-05-06                                     == ano, mês e ano
* 11:04:32.102686                                == hora, minuto, segundo, frações de segundos
* IP (...)                                       == informações sobre o IP
  1. IP (tos 0x10, ...)                          == type of service
  2. IP (..., ttl 64, ...)                       == time to live
  3. IP (..., id 40256, ...)                     == número de identificação (acknowledgment number) do IP
  4. IP (..., offset 0, ...)                     == data offset
  5. IP (..., flags [DF], ...)                   == flags TCP
  6. IP (..., proto TCP (6), ...)                == tipo de protocolo que IP carrega
  7. IP (..., length 60)                         == tamanho do IP
* 127.0.0.1.50688                                == IP Client, numa porta aleatória (socket de origem)
* >                                              == mostra o fluxo de envio do IP
* 127.0.0.1.81                                   == IP Server, na porta estabelecido no nc 
* :                                              == separação de informações, aqui protocolo IP
* Flags [S]                                      == flag (SYN) enviada do Client ao Server, para estabelecer a conexão
* cksum 0xfe34 (incorrect -> 0xd4cd)             == cksum TCP
* seq 810775634                                  == número de sequência
* win 65495                                      == reserva de buffer, em geral, começa com número baixo e vai crescendo até estabilizar
* options [...]                                  == seta as opções para utilizar com os protocolos IP
  1. options [..., TS val 2518989874 ecr 0, ...] == Time Stamp e valor decorrido desde algum ponto (depende do OS) | Echo Reply: time stamp enviado e retornado, só que do lado do SERVER
  2. options [..., wscale7]                      == potencializa janela de bytes para as próximas janelas que NÂO sâo SYN: win <NUM> ^ 7
* length 0                                       == tamanho do payload, como não existe payload, o tamanho é zero


> Solicitação de conexão do Client ao Server
* 2022-05-06                                     == ano, mês e ano
* 11:04:34.50688                                 == hora, minuto, segundo, frações de segundos
* IP (...)                                       == informações sobre o IP
  1. IP (tos 0x10, ...)                          == type of service
  2. IP (..., ttl 64, ...)                       == time to live
  3. IP (..., id 40256, ...)                     == número de identificação (acknowledgment number) do IP
  4. IP (..., offset 0, ...)                     == data offset
  5. IP (..., flags [DF], ...)                   == flags TCP
  6. IP (..., proto TCP (6), ...)                == tipo de protocolo que IP carrega
  7. IP (..., length 60)                         == tamanho do IP
* 127.0.0.1.50688                                == IP Client, numa porta aleatória (socket de origem)
* >                                              == mostra o fluxo de envio do IP
* 127.0.0.1.81                                   == IP Server, na porta estabelecido no nc 
* :                                              == separação de informações, aqui protocolo IP
* Flags [S]                                      == flag (SYN) enviada do Client ao Server, para estabelecer a conexão
* cksum 0xfe34 (incorrect -> 0xcced)             == cksum TCP
* seq 810775634                                  == número de sequência
* win 65495                                      == reserva de buffer, em geral, começa com número baixo e vai crescendo até estabilizar
* options [...]                                  == seta as opções para utilizar com os protocolos IP
  1. options [..., TS val 2519456429 ecr 0, ...] == Time Stamp e valor decorrido desde algum ponto (depende do OS) | Echo Reply: time stamp enviado e retornado, só que do lado do SERVER
  2. options [..., wscale7]                      == potencializa janela de bytes para as próximas janelas que NÂO sâo SYN: win <NUM> ^ 7
* length 0                                       == tamanho do payload, como não existe payload, o tamanho é zero


---


## Tráfego TCP Anômalo
Anômalo por 1 desses motivos:
* perda de pacote IP
* pacote IP chegaram fora de ordem

## TCPDUMP
Em um terminal (tty) - ou emulador de terminal (pts), ou aba etc.
*      -n        == não resolva nome
*      -v        == mostra informações sobre o IP
* -w <FILE>.pcap == grava saída em um arquivo
*     port       == as portas que devem estar a escuta
```
  sudo tcpdump -n -v -w <FILE>.pcap port 80
```

Uma vez que já tenha sido realizada a captura, exiba-a:
*      -n        == não resolva nome
* -r <FILE>.pcap == leia arquivo
*      -S        == números de sequência absolutos
*    cat -n      == número as linhas do arquivo
* sed 's/^/\n/'  == pule uma linha
*     less       == permite mover-se pelo fluxo tcp
```
  sudo tcpdump -n -r <FILE>.pcap -S | cat -n | sed 's/^/\n/' | less
```

### Exemplo de captura através do tcpdump
```
  tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
  listening on lo, link-type EN10MB (Ethernet), snapshot length 262144 bytes

 1 2022-05-06 22:23:01.994556 IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [S], seq 1160318600, win 5840, options [mss 1460,sackOK,TS val 2538826 ecr 0,nop,wscale 6], length 0

 2  2022-05-06 22:23:01.994605 IP 74.55.41.178.80 > 172.21.12.159.54639: Flags [S.], seq 2428369942, ack 1160318601, win 65483, options [mss 1460], length 0
 
 3  2022-05-06 22:23:01.909380 IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [.], ack 2428369943, win 5840, length 0
 
 4  2022-05-06 22:23:04.220509 IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [P.], seq 1160318601:1160318608, ack 2428369943, win 5840, length 7: HTTP: GET h
 
 5  2022-05-06 22:23:05.220591 IP 74.55.41.178.80 > 172.21.12.159.54639: Flags [.], ack 1160318608, win 5840, length 0
 
 6  2022-05-06 22:23:05.220607 IP 74.55.41.178.80 > 172.21.12.159.54639: Flags [F.], seq 2428372010, ack 1160318608, win 5840, length 0
 
 7  2022-05-06 22:23:05.223374 IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [.], ack 2428369943, win 5840, length 0
 
 8  2022-05-06 22:23:05.223381 IP 74.55.41.178.80 > 172.21.12.159.54639: Flags [P.], seq 2428371403:2428372010, ack 1160318608, win 5840, length 607: HTTP
 
 9  2022-05-06 22:23:05.229617 IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [.], ack 2428369943, win 5840, length 0
 
10  2022-05-06 22:23:05.229632 IP 74.55.41.178.80 > 172.21.12.159.54639: Flags [P.], seq 2428369943:2428371403, ack 1160318608, win 5840, length 1460: HTTP

11  2022-05-06 22:23:05.229632 IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [.], ack 2428372011, win 8760, length 0

12  2022-05-06 22:23:05.231280 IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [F.], seq 1160318608, ack 2428372011, win 8760, length 0

13  2022-05-06 22:23:05.220591 IP 74.55.41.178.80 > 172.21.12.159.54639: Flags [.], ack 1160318609, win 5840, length 0
```

> **OBS**: novamente, este é um exemplo de reetransmissão rápida

#### Interpretação da saída
CLIENT conecta ao server 
Flag: SYN
seq:  meu número de sequência (iniciamente aleatório): seq 1160318600
```
1  IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [S] seq 1160318600
```

SERVER responde e envia ao CLIENT: 
Flag: ACK-SYN
seq:  meu número de sequência é: seq 2428369942
ack:  espero que seu próximo número de sequência enviado seja: ack 1160318601
```
2  IP 74.55.41.178.80 > 172.21.12.159.54639: Flags[S.] seq 2428369942, ack 1160318601
```

CLIENT responde ao SERVER:
Flag: ACK. 
seq:  como Ack não é Flag, não possui número de sequência
ack:  espero que seu próximo número de sequência enviado seja: ack 2428369943
```
3  IP 172.21.12.159.54639 > 74.55.41.178.80 Flags [.], ack 2428369943
```

CLIENT envia payload ao SERVER:
Flag: ACK-PSH (Push)
seq:  meu número de sequência é: seq 1160318601, estimo que o próximo seja: 1160318608
ack:  espero que seu próximo número de sequência enviado seja: ack 2428369943
```
4  IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [P.], seq 1160318601:1160318608, ack 2428369943, win 5840, length 7: HTTP: GET h
```

SERVER responde ao CLIENT: 
Flag: ACK
seq:  como Ack não é Flag, não possui número de sequência
ack:  espero que seu próximo número de sequência enviado seja: ack 1160318608
```
5  IP 74.55.41.178.80 > 172.21.12.159.54639: Flags [.], ack 1160318608, win 5840, length 0
```

SERVER responde e envia ao CLIENT: 
Flag: ACK-FYN
seq:  meu número de sequência é: seq 2428372010
ack:  espero que seu próximo número de sequência enviado seja: ack 1160318608
```
6  IP 74.55.41.178.80 > 172.21.12.159.54639: Flags [F.], seq 2428372010, ack 1160318608, win 5840, length 0
```

> Expectativa: SERVER > CLIENT: Flags [P.], seq 2428369943
┌─────────────────────────────────────────────────────────────────────────────────────┐
│  Como o SERVER respondeu a um request (requisição) do CLIENT                        │
│  com um FYN (desejado: PSH)                                                         │
│  e um número de sequência não esperado (esperado: 2428369943 | recebido: 2428372010)│
│                                                                                     │
│  O CLIENT avalia a conexão (socket de origem e socket de destino)                   │
│  se for a mesma conexão, O CLIENT guarda essa informação no buffer.                 │
│                                                                                     │
│  Em seguida, CLIENT pede a reetransmissão (reetransmissão a pedido)                 │
│  do que não fora entregue, até que o valor do ACK seja o esperado                   │
│                                                                                     │
│  No caso, o número especificado no campo "Acknowledgment Number" do TCP do CLIENT   │
│  que é o número de sequência do SERVER esperado pelo CLIENT                         │
└─────────────────────────────────────────────────────────────────────────────────────┘

CLIENT responde ao SERVER:
Flag: ACK
seq:  como Ack não é Flag, não possui número de sequência
ack:  espero que seu próximo número de sequência enviado seja: ack 2428369943
```
7  IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [.], ack 2428369943, win 5840, length 0
```

SERVER responde e envia payload ao CLIENT: 
Flag: ACK-PSH (Push)
seq:  meu número de sequência é: seq 2428371403, estimo que o próximo seja: 2428372010
ack:  espero que seu próximo número de sequência enviado seja: ack 1160318608
```
8  IP 74.55.41.178.80 > 172.21.12.159.54639: Flags [P.], seq 2428371403:2428372010, ack 1160318608, win 5840, length 607: HTTP
```

> Expectativa: SERVER > CLIENT: Flags [P.], seq 2428369943
┌─────────────────────────────────────────────────────────────────────────────────────┐
│  Como o SERVER respondeu a um request (requisição) do CLIENT                        │
│  com um número de sequência diferente (esperado: 2428369943 | recebido: 2428371403) │
│  o CLIENT guarda essa informação no buffer.                                         │
│                                                                                     │
│  O próximo número de sequência que se estima receber, 2428372010                    │
│  também já foi armazenado no buffer anteriormente (linha 6).                        │
│                                                                                     │
│  Diante disso, CLIENT pede a reetransmissão (reetransmissão a pedido)               │
│  do que não fora entregue:                                                          │
│  número especificado no campo "Acknowledgment Number" do TCP do CLIENT              │
│  que é o número de sequência SERVER esperado pelo CLIENT                            │
└─────────────────────────────────────────────────────────────────────────────────────┘

CLIENT responde ao SERVER:
Flag: ACK
seq:  como Ack não é Flag, não possui número de sequência
ack:  espero que seu próximo número de sequência enviado seja: ack 2428369943
```
9  IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [.], ack 2428369943, win 5840, length 0
```

SERVER responde envia payload ao CLIENT: 
Flag: ACK-PSH (Push) **OBS**: o P não é mostrado, mas possui payload então é um Push
seq:  meu número de sequência é: seq 2428369943, estimo que o próximo seja: 2428371403
ack:  espero que seu próximo número de sequência enviado seja: ack 1160318608
```
10  IP 74.55.41.178.80 > 172.21.12.159.54639: Flags [.], seq 2428369943:2428371403, ack 1160318608, win 5840, length 1460: HTTP
```

CLIENT responde ao SERVER:
Flag: ACK
seq:  como Ack não é Flag, não possui número de sequência
ack:  espero que seu próximo número de sequência enviado seja: ack 2428372011
```
11  IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [.], ack 2428372011, win 8760, length 0
```
┌─────────────────────────────────────────────────────────────────────────────┐
│ Como CLIENT recebeu o número de sequência desejado:    2428369943 (linha 10)│
│ e próximo número de sequência também já fora recebido: 2428371403 (linha  8)│
│ e próximo número de sequência também já fora recebido: 2428372010 (linha  6)│
│                                                                             │
│ O CLIENT requisita o próximo número de sequência do SERVER: ack 2428372011  │
└─────────────────────────────────────────────────────────────────────────────┘
                                                                              
CLIENT responde e envia ao SERVER:                                          
Flag: ACK-FYN                                                                  
seq:  meu número de sequência é: seq 1160318608                                
ack:  espero que seu próximo número de sequência enviado seja: ack 2428372011  
```
12  IP 172.21.12.159.54639 > 74.55.41.178.80: Flags [F.], seq 1160318608, ack 2428372011, win 8760, length 0
```

SERVER responde ao CLIENT: 
Flag: ACK
seq:  como Ack não é Flag, não possui número de sequência
ack:  espero que seu próximo número de sequência enviado seja: ack 1160318609
```
13  IP 74.55.41.178.80 > 172.21.12.159.54639: Flags [.], ack 1160318609, win 5840, length 0
```

### Entendimnto da entrega dos pacotes IP
Agora, busca-se identicar se houve perda de pacote, ou se chegaram fora de ordem

Uma vez que já tenha sido realizada a captura, exiba-a:
*      -n        == não resolva nome
* -r <FILE>.pcap == leia arquivo
*      -S        == números de sequência absolutos
*      -v        == informações sobre o IP
*    cat -n      == número as linhas do arquivo
* sed 's/^/\n/'  == pule uma linha
*     less       == permite mover-se pelo fluxo tcp
```
  sudo tcpdump -n -r <FILE>.pcap -S -v | cat -n | sed 's/^/\n/' | less
```

### Exemplo de captura através do tcpdump com informações do IP
```
  tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
  listening on lo, link-type EN10MB (Ethernet), snapshot length 262144 bytes

 1 2022-05-06 22:23:01.994556 IP (tos 0x10, ttl 64, id 46018, offset 0, flags [DF], proto TCP (6), length 60)
     172.21.12.159.54639 > 74.55.41.178.80: Flags [S], cksum 0x1db2 (correct), seq 1160318600, win 5840, options [mss 1460,sackOK,TS val 2538826 ecr 0,nop,wscale 6], length 0

 2  2022-05-06 22:23:01.994605 IP (tos 0x0, ttl 50, id 0, offset 0, flags [DF], proto TCP (6), length 44)
     74.55.41.178.80 > 172.21.12.159.54639: Flags [S.], cksum 0x9e62 (correct), seq 2428369942, ack 1160318601, win 65483, options [mss 1460], length 0
 
 3  2022-05-06 22:23:01.909380 IP (tos 0x10, ttl 64, id 46019, offset 0, flags [DF], proto TCP (6), length 40)
     172.21.12.159.54639 > 74.55.41.178.80: Flags [.], cksum 0xb61f (correct), ack 2428369943, win 5840, length 0
 
 4  2022-05-06 22:23:04.220509 IP (tos 0x10, ttl 64, id 46020, offset 0, flags [DF], proto TCP (6), length 47)
     172.21.12.159.54639 > 74.55.41.178.80: Flags [P.], cksum 0xa89d (correct), seq 1160318601:1160318608, ack 2428369943, win 5840, length 7: HTTP: GET h
 
 5  2022-05-06 22:23:05.220591 IP (tos 0x0, ttl 50, id 20038, offset 0, flags [DF], proto TCP (6), length 40)
     74.55.41.178.80 > 172.21.12.159.54639: Flags [.], cksum 0xb618 (correct), ack 1160318608, win 5840, length 0
 
 6  2022-05-06 22:23:05.220607 IP (tos 0x0, ttl 50, id 20041, offset 0, flags [DF], proto TCP (6), length 40)
     74.55.41.178.80 > 172.21.12.159.54639: Flags [F.], cksum 0xae04 (correct), seq 2428372010, ack 1160318608, win 5840, length 0
 
 7  2022-05-06 22:23:05.223374 IP (tos 0x10, ttl 64, id 46021, offset 0, flags [DF], proto TCP (6), length 40)
     172.21.12.159.54639 > 74.55.41.178.80: Flags [.], cksum 0xb618 (correct), ack 2428369943, win 5840, length 0
 
 8  2022-05-06 22:23:05.223381 IP (tos 0x0, ttl 50, id 20040, offset 0, flags [DF], proto TCP (6), length 647)
     74.55.41.178.80 > 172.21.12.159.54639: Flags [P.], cksum 0xe4c5 (correct), seq 2428371403:2428372010, ack 1160318608, win 5840, length 607: HTTP
 
 9  2022-05-06 22:23:05.229617 IP (tos 0x10, ttl 64, id 46022, offset 0, flags [DF], proto TCP (6), length 40)
     172.21.12.159.54639 > 74.55.41.178.80: Flags [.], cksum 0xb618 (correct), ack 2428369943, win 5840, length 0
 
10  2022-05-06 22:23:05.229632 IP (tos 0x0, ttl 50, id 20039, offset 0, flags [DF], proto TCP (6), length 1500)
      74.55.41.178.80 > 172.21.12.159.54639: Flags [P.], cksum 0xbf1b (correct), seq 2428369943:2428371403, ack 1160318608, win 5840, length 1460: HTTP

11  2022-05-06 22:23:05.229632 IP (tos 0x10, ttl 64, id 46023, offset 0, flags [DF], proto TCP (6), length 40)
      172.21.12.159.54639 > 74.55.41.178.80: Flags [.], cksum 0xa29c (correct), ack 2428372011, win 8760, length 0

12  2022-05-06 22:23:05.231280 IP (tos 0x10, ttl 64, id 46024, offset 0, flags [DF], proto TCP (6), length 40)
      172.21.12.159.54639 > 74.55.41.178.80: Flags [F.], cksum 0xa29b (correct), seq 1160318608, ack 2428372011, win 8760, length 0

13  2022-05-06 22:23:05.220591 IP (tos 0x0, ttl 50, id 20042, offset 0, flags [DF], proto TCP (6), length 40)
      74.55.41.178.80 > 172.21.12.159.54639: Flags [.], cksum 0xae03 (correct), ack 1160318609, win 5840, length 0
```

Como a anomalia foi detectada no lado SERVER,
apenas será avaliado o ID de identificação dos pacotes IP
advindos deste lado

**OBS**: id do SERVER começou com 0, o Linux não segue a RFC

1. linha  2: id 0
2. linha  5: id 20038
3. linha  6: id 20041
4. linha  8: id 20040
5. linha 10: id 20039
6. linha 13: id 20042

Como não há furo, não há buraco, i. e.
TODOS OS NÙMEROS DE IDENTIFICAÇÂO DA SEQUÊNCIA ESTÂO PRESENTES
Então, não houve perda de pacote.

Logo, os pacotes IP chegaram fora de ordem.

---

# Exemplo ARP

## Exemplo 1

### com tcpdump
* -n 				= não resolve nome
* arp       = procura protocolo ARP
```
  sudo tcpdump -n arp
```

#### Saída do tcpdump para ARP
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

#### Análise da saída do tcpdump
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

## Exemplo 1

### com ping
Em um terminal (tty) - ou emulador de terminal (pts), ou aba etc.  
```
  ping 192.168.0.100
```

### com tcpdump
Em outro terminal (tty) - ou emulador de terminal (pts), ou aba etc.  

* -n 				  = não resolve nome
* host        = IP a ser capturado
* -e          = exibe link-level, camada 2 (Ethernet e IEEE 802.11)
```
  sudo tcpdump -n host 192.168.0.100 -e
```

#### Saída do tcpdump para ARP
* Resquest          = requisição feita por alguma máquina em rede
*  Reply            = resposta a uma requisição (request)
```
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on enp2s0, link-type EN10MB (Ethernet), snapshot length 262144 bytes

16:15:16.594492 40:16:7e:bb:8e:16 > e8:40:f2:c3:7f:6e, ethertype IPv4 (0x0800), length 98: 
192.168.0.180 > 192.168.0.100: ICPM echo request, id 15864, seq 99, length 64

16:15:16.594667 e8:40:f2:c3:7f:6e > 40:16:7e:bb:8e:16, ethertype IPv4 (0x0800), length 98: 
192.168.0.100 > 192.168.0.180: ICPM echo reply, id 15864, seq 99, length 64

16:15:17.618485 40:16:7e:bb:8e:16 > e8:40:f2:c3:7f:6e, ethertype IPv4 (0x0800), length 98: 
192.168.0.180 > 192.168.0.100: ICPM echo request, id 15864, seq 100, length 64

16:15:17.618654 e8:40:f2:c3:7f:6e > 40:16:7e:bb:8e:16, ethertype IPv4 (0x0800), length 98: 
192.168.0.180 > 192.168.0.100: ICPM echo reply, id 15864, seq 100, length 64

16:15:18.642447 40:16:7e:bb:8e:16 > e8:40:f2:c3:7f:6e, ethertype IPv4 (0x0800), length 98: 
192.168.0.180 > 192.168.0.100: ICPM echo request, id 15864, seq 101, length 64

16:15:18.642593 e8:40:f2:c3:7f:6e > 40:16:7e:bb:8e:16, ethertype IPv4 (0x0800), length 98: 
192.168.0.180 > 192.168.0.100: ICPM echo reply, id 15864, seq 101, length 64
```

#### Detalhamento de linha do tcpdump
> Envio de ping do MAC Address de origem para o MAC Address de destino
* 16:15:16.594492        == hora, minuto, segundo,frações de segundos
* 40:16:7e:bb:8e:16      == MAC Address de origem
* >                      == mostra o fluxo de envio do IP
* e8:40:f2:c3:7f:6e      == MAC Address de destino
* ethertype              == tipo de protocolo carregado dentro do payload
* IPv4 (0x0800)          == representação em hexadecimal do protocolo
* length 98              == tamanho do frame Ethernet (payload)
* :                      == separação de informações, aqui fim do protocolo Ethernet e começo do IP
* 192.168.0.180          == IP de origem
* 192.168.0.100          == IP de destino
* :                      == separação de informações, aqui fim do protocolo IP e começo do ICMP
* ICMP echo request      == envio de um datagrama que espera uma resposta (ICMP echo reply)
* id 15864               == número de identificação do ICMP, que não muda
* seq 99                 == número de sequência do ICMP, que muda
* length 64              == tamanho do pacote IP (payload)


> Resposta ao ping do MAC Address de destino para o MAC Address de origem
* 16:15:16.594667        == hora, minuto, segundo,frações de segundos
* e8:40:f2:c3:7f:6e      == MAC Address de origem
* >                      == mostra o fluxo de envio do IP
* 40:16:7e:bb:8e:16      == MAC Address de destino
* ethertype              == tipo de protocolo carregado dentro do payload
* IPv4 (0x0800)          == representação em hexadecimal do protocolo
* length 98              == tamanho do frame Ethernet (payload)
* :                      == separação de informações, aqui fim do protocolo Ethernet e começo do IP
* 192.168.0.100          == IP de origem
* 192.168.0.180          == IP de destino
* :                      == separação de informações, aqui fim do protocolo IP e começo do ICMP
* ICMP echo reply        == resposta com datagrama (ICMP echo reply) a uma requisição (ICMP echo reply)
* id 15864               == número de identificação do ICMP, que não muda
* seq 99                 == número de sequência do ICMP, que muda
* length 64              == tamanho do pacote IP (payload)


#### Análise da saída do tcpdump
Abaixo, o MAC Address **40:16:7e:bb:8e:16** envia ao MAC Address **e8:40:f2:c3:7f:6e** um ping 
cujo IP de origem é **192.168.0.180** e o IP de destino é: **192.168.0.2** um datagrama ICMP echo request. 
Um ping a um IP é enviado e espera uma resposta da máquina com o este IP
```
16:15:16.594492 40:16:7e:bb:8e:16 > e8:40:f2:c3:7f:6e, ethernet IPv4 (0x0800), length 98: 
192.168.0.180 > 192.168.0.100: ICPM echo request, id 15864, seq 99, length 64
```

O MAC Address **e8:40:f2:c3:7f:6e** responde a requisição (ICMP echo request)
do MAC Address **40:16:7e:bb:8e:16** com o um ICMP echo Reply: ping-pong.
```
16:15:16.594667 e8:40:f2:c3:7f:6e > 40:16:7e:bb:8e:16, ethertype IPv4 (0x0800), length 98: 
192.168.0.100 > 192.168.0.180: ICPM echo reply, id 15864, seq 99, length 64
```
