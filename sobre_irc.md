# IRSSI
Client IRC

## IRSSI install (Debian)
```
  apt install irssi
```
## Arquivo de configuração
```
  "${HOME}/.irssi/config"
```

## Adicionar server
```
  /server add <APELIDO> <NOME DO SERVER> <PORTA> <PASSWORD>
```
  Exemplo, utilizado o server (rede do IRC) Libera.chat
  ```
    /server add libera irc.libera.chat 6692 <PASSWORD>
  ```
  Exemplo, utilizado o server (rede do IRC) Slackjeff.com.br
  ```
    /server add Slackjeff slackjeff.com.br 6697 <PASSWORD>
  ```
  Exemplo com aliases (network), tls e ssl configurados
  ```
    /server add -ssl -ssl_verify -tls -network Libera irc.libera.chat 6697
  ```
  Exemplo com aliases (network), tls e ssl configurados
  ```
    /server add -ssl -ssl_verify -ssl_capath /etc/ssl/certs -network freenode irc.freenode.net 6697 password
  ```

## Remover server
```
  /server remove <NOME DO SERVER>
```
  Exemplo, utilizado o server (rede do IRC) Libera.chat
  ```
    /server remove irc.libera.chat
  ```

## Adicinar criptografia em uma conexão a um SERVER
Dentro do arquivo de configuração, procure um SERVER.
Exemplo, Freenode:
```
  servers = (
  ...
  {
    address = "chat.freenode.net";
    chatnet = "Freenode";
    port = "6667";
  },
  ...
```
Agora, adicione as seguintes linhas:
```
  servers = (
  ...
  {
    address = "chat.freenode.net";
    chatnet = "Freenode";
    use_ssl = "yes";
    ssl_verify = "yes";
    port = "6667";
  },
  ...
```
Além disso, mude a porta de acesso:
```
  servers = (
  ...
  {
    address = "chat.freenode.net";
    chatnet = "Freenode";
    use_ssl = "yes";
    ssl_verify = "yes";
    port = "6697";
  },
  ...
```
Neste mesmo arquivo, pode-se definir o nickname a ser usado.
Vá até o final do arquivo e procure por:
```
  settings = {
    core = {
      real_name = "<MEU NOME>";
      user_name = "<NICKNAME>";
      nick = "<NICKNAME>";
    };
  ...
```


# COMANDOS BÁSICOS
Listar servidores
```
  /server list
```

Realizar a conexão
```
  /connect <NOME DO SERVER>
  /connect chat.freenode.net
  /connect freenode
```

Realizar desconexão
```
  /disconnect
```

Mudança de nickname
```
  /nick <NOVO NICKNAME>
  /nick taquigrafismo
```

Registrar nickname
```
  /msg nickserv register <MEU PASSWORD> <MEU EMAIL>
```

Autenticar nickname (verifique email)
```
  /msg nickserv identify <MEU PASSWORD>
```

(Após verificar email)
```
  /msg NickServ VERIFY REGISTER <NOVO NICKNAME> <MEU PASSWORD>
```

Autoconectar a um servidor
```
  /network add -autosendcmd "/msg nickserv identify <MEU PASSWORD> ; wait 400" <NOME DA SERVER>
```

Conectar num canal
```
  /join <NOME DO CANAL>
  /join #mazonos
```
Ou:
```
  /join ##mazonos
```

Fechar (Sair) canal
```
  /leave
```

Verificar nomes de usuários
```
  PageUP
  PageDown
  /name
```

Mandar mensagem
```
  <NOME DE QUEM VAI RECEBER><TAB> <MENSAGEM>
```

Mensagem privada
```
  /query <NOME DE QUEM VAI RECEBER> <MENSAGEM>
  /msg <NOME DE QUEM VAI RECEBER> <MENSAGEM>
```

Lista janelas (buffers) aberta(o)s
```
  /window list
```

Fechar janela (buffer)
```
  /window close
```

Mudar de janelas (buffer)
```
  ALT+<NÚMERO DO BUFFER>
```
  Dentro do IRSSI
  ```
    /<NÚMERO DO BUFFER>
  ```

Apagar as informações em tela
```
  /clear
```

Demonstrar ausência
```
  /away <MENSAGEM>
```
Também serve para demonstrar retorno:
```
  /away
```

Sair do IRSSI
```
  /quit
```



# WEECHAT
## Suporte a mouse
```
  /mouse enable
```

## Adicionar server
```
  /server add libera irc.libera.chat/6697 -ssl
```

Fechar janela (buffer)
```
  /close
```

[](https://weechat.org/doc/user/)
[](https://gist.github.com/chirag64/3c80a08a7fc1d2c52ea0)
