# RTFL 
  **Read The Fantastic Logs**

# LUGAR DOS LOGS
```sh
  cd /var/log/
```

# PORTA DOS LOGS
```sh
   printf "$(< /etc/services)" # portas padrão dos sistema
   printf "$(< /usr/etc/services)" # portas padrão dos sistema
```

---------------------------------------------------

# RSYSLOG


## Arquivo de logs
  * .log        # logs dos sistema
  * auth.log    # aceso
  * rsyslog.log # gerencia arquivo de log
  * user.log    # logs do usuário


## RSyslog
> utilitário do sistema para prover suporte a mensagens de logs (syslogd extendido)
```sh
  /etc/rsyslog.conf              # Debian
  		ou
  /etc/rsyslog.d/50-default.conf # Ubuntu
```


## Dentro do arquivo RSyslog ou Syslog
```sh
  tail -f /var/log/syslog
  		ou
  tail -f /var/log/rsyslog
```


## Estrutura
```sh
  data | host que gerou o log | serviço | mensagem
```


## Facilidade.Prioridade (nível)

  > NÂO SE PODE CRIAR NOVAS FACILIDADES, são um número pré-definido

  > Pode-se customizar facilidade entre os:
    * LOCAL0-LOCAL7

  > Lista de Prioridades (aplicação quem decide)
  ```sh
    gera menos mensagens    | emerg
              | alert
              | crit
              | err
              | warn
              | notice
              | info
   gera mais mensagens     | debug
  ```

  ### EX das regras de logs:
    * OBS: - == desativa a sincronização imediata do arquivo após sua gravação
    ```sh
      kernel.*          -/var/log/kern.log # log kernel
      mail.*            -/var/log/mail.log # log email
      user.*            -/var/log/user.log # log usuário
    ```

  ### Ex de criação de regras de logs:
    > Utilização do editor vi, pode ser qualquer outro.
    ```sh
      vi /etc/rsyslog.conf
          ou
      vi /etc/rsyslog.d/50-default.conf
    ```

    > Qualquer facilidade e qualquer prioridade (*.*), todas as mensagens.
    ```sh
      *.*               -/var/log/catatudo.log  # Em: First...
    ```

    > Utilização do Systemd.
    ```sh
      systemctl status rsyslog.service          # verifica status
      systemctl restart rsyslog.service         # reinicia estado
    ```

    > Ao diretório de logs.
    ```sh
      ls /var/log/                              # procura por catatudo.log
    ```

  ### OBS
    * ,  # agrupa mais de uma facilidade na mesma linha (Concatena)
    * ;  # permite separar facilidades.prioridade diferentes (Agrupamento)
    * *  # redirecione todas as mensagens da faiclidade
    * =  # somente o nível especificado será registrado (nem acima e nem abaixo)
    * @  # máquina remota udp
    * @@ # máquina remota tcp

      #### Ex
        > uma prioridade.facilidade ; uma prioridade.facilidade
        ```sh
          auth.info;user.info         -/var/log/auth_user.log
        ```

        > uma prioridade.facilidade ; duas prioridades com uma facilidade (tudo de usuário e nada de autenticação)
        ```sh
          user.*;auth,authpriv.none   -/var/log/user_no_auth.log
        ```

        > Todos os logs para uma máquina remota
        ```sh
          *.*                         @192.168.86.49
        ```

        > facilidades.=somente o nível especificado ;
          prioridade,prioridade.facilidade ;
          prioridade.facilidade ; prioridade.facilidade
        > - # desativa a sincronização imediata do arquivo após sua gravação
        ```sh
          *.=debug;\
             auth,authpriv.none;\
             news.none;mail.none      -/var/log/debug
        ```

---------------------------------------------------

# JOURNALCTL
> Mostra informações do boot atual
```sh
  journalctl -b
```

> Mostra os erros de um serviço
```sh
  journalctl -b -u <SERVIÇO>
```

> Mostra os erros
```sh
  journalctl -xe
```

```sh
	journalctl --utc
```

> Mensagens das últimas duas (2) horas
```sh
	journalctl --since "2 hour ago"
```

> Mensagens dos últimos dois (2) dias
```sh
	journalctl --since "2 days ago"
```

> Mensagens dos últimos dois (2) dias até as últimas duas (2) horas
```sh
	journalctl --since "2 days ago" --until "2 hours ago"
```

> Mensagens do dia 9 do mês 10 de 2021 às 1 da manhã
```sh
	journalctl --since "2021-10-09 01:00:00"
```

> Apenas mensagens sobre o kernel
```sh
	journalctl -k
```

> -u <SERVIÇO>, mostra logs apenas daquele serviço pedido
```sh
	journalctl -u <SERVIÇO>
```

> Segue os serviços e mostra últimas linhas == tail -f
```sh
	journalctl -f
```

> número de últimas linhas == tail -f
```sh
	journalctl -n
```

> mostra na ordem reversa
```sh
	journalctl -r
```

> especifica a saída, por exemplo: -o json-pretty
```sh
	journalctl -o <FORMATO>
```

> especifica a prioridade a ser exibida, por exemplo: -p emerg..err
```sh
	journalctl -p <PRIORIDADE>
```

> Mensagens relacionados apenas ao UID do usuário, por exemplo: _UID=1000
```sh
	journalctl _UID=<NÚMERO DO UID>
```

## Erros Identificados
  tracker-store.service
  SQLite error: database disk image is malformed (errno: Recurso temporariamente indisponível)

---------------------------------------------------

# REFERÊNCIAS
  [Guia Foca Linux - Cap. 17](https://guiafoca.org/guiaonline/seguranca/ch03.html)
  [Linux Tips]()
  [NLog.Targets.Syslog-Personal](https://github.com/luigiberrettini/NLog.Targets.Syslog-Personal/blob/master/docs/syslog-message-format.md)
