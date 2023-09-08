# Mutt
## Configurações (para ler email online)
### Local no qual rezidem as configurações
```
  mkdir -p "${HOME}/.config/mutt"
  touch "${HOME}/.config/mutt/.muttrc"
```

### Dentro do .muttrc
```
  # Segurança
  set ssl_starttls="yes"
  set ssl_force_tls="yes"

  # Chave GPG
  # source "${HOME}/.config/mutt/gpg.rc"
  # source gpg.rc

  # Cores
  source "${HOME}/.config/mutt/cores.muttrc"
  # source cores.muttrc

  # Imap crendetials
  set imap_user="MEU-EMAIL@gmail.com"
  set imap_pass='MINHA_SENHA'

  # Smtp crendetials
  # set smtp_url="smtps://MEU-EMAIL@gmail.com:MINHA_SENHA@smtp.gmail.com:465/" # email + senha
  set smtp_url="smtps://MEU-EMAIL@gmail.com@smtp.gmail.com:465/"
  set smtp_pass='MINHA_SENHA'

  # Sobre mim
  set from="MEU-EMAIL@gmail.com"
  set realname="MEU_NOME"

  # Signature
  set signature="${HOME}/.config/mutt/.assinatura.sig"

  # set folder="imaps://imap.gmail.com/:993" # Caixa de correio
  # set spoolfile="imaps://imap.gmail.com/INBOX" # Especifica localização da caixa de correio
  set folder="imaps://imap.gmail.com/" # Caixa de correio
  set spoolfile="+INBOX" # Especifica localização da caixa de correio de forma simplificada

  # Especifica o arquivo em que minhas mensagens de saída devem ser anexadas
  set record="imaps://MEU-EMAIL@imap.gmail.com/Sent"

  # Ao optar por adiar uma mensagem, Mutt a salva na caixa de correio especificada por esta variável.
  # set postponed="imaps://imap.gmail.com/[Gmail]/Drafts"

  # Update buffers
  # set timeout=20 # 20 segundos

  # Especifica a pasta em que ler correio em sua pasta $spoolfile será anexado
  # set mbox="+INBOX"

  # Controla se o Mutt vai enviar mensagens da spool mailbox para mbox mailbox
  set move="no"

  # Controla o tempo (em segundos) em que o Mutt espera antes de sondar conexões IMAP abertas, 
  # para evitar que o servidor as feche antes que o Mutt tenha terminado com eles.
  set mail_check=60
  set imap_keepalive="900"

  # Conjunto de caracteres em mensagens enviadas
  set send_charset="utf-8"

  # Caso não haja nenhum conjunto de caracteres fornecido nas mensagens recebidas, faz-se provável que seja Windows
  set assumed_charset="iso-8859-1"

  # Certifique-se de que o Vim sabe que o Mutt é um cliente de email e uma mensagem UTF-8 será codificada
  set editor="vim -c 'set syntax=mail ft=mail enc=utf-8'"

  # Basta percorrer uma linha em vez da página completa
  set menu_scroll=yes

  # Queremos ver alguns tipos MIME inline
  auto_view application/msword
  auto_view application/pdf

  # Faça o padrão de busca ser em To, Cc e Subject
  set simple_search="-f %s | -C %s | -s %s"

  # Classificar por tópicos
  set sort_aux=last-date-received
  # set sort=threads
  set sort=reverse-threads
  set sort_re
  set strict_threads=yes

  # Marcar como Spam ao ler uma mensagem
  spam "X-Spam-Score: ([0-9\\,]+).*" "SA: %1"
  set pager_format = " %C - %[%H:%M] %.20v, %s%* %?H? [%H] ?"

  # Não mostra todos os cabeçalhos, apenas os que desejar
  ignore          *
  unignore        From To Cc Bcc Date Subject
  # e nesta ordem
  unhdr_order     *
  hdr_order       From: To: Bcc: Date: Subject:

  # Configurações pessoais
  # alternates "MEU-EMAIL@gmail.com|MEU-OUTRO-EMAIL@gmail.com"

  # descomente a linha abaixo se você deseja usar: catálogo de endereços
  #source ~/.aliases

  # Use headercache para IMAP (certifique-se de que este é um diretório para melhor desempenho!)
  set header_cache="/var/tmp/.mutt"

  # Descomente isso para ativar o recurso da barra lateral
  #set sidebar_visible = yes
  set sidebar_width = 15
  set sidebar_folder_indent = yes
  set sidebar_short_path = yes

  # Faça as atualizações de progresso não tão caras, isso atualizará a barra a cada 300ms
  set read_inc = 1
  set time_inc = 300

  # somente se você compilou o Mutt com gpgme, habilite o back gpgme
  # set crypt_use_gpgme = yes
  # você pode configurar isso para ocultar a saída de verificação do gpg e apenas confiar na FLAG de estado do Mutt
  #set crypt_display_signature = no

  # habilitar a assinatura de e-mails por padrão
  #set pgp_autosign = yes
  #set pgp_sign_as = 0xXXXXXXXX   # seu keypad gpg aqui
  #set pgp_replyencrypt = yes

  # Entradas que queremos monitorar para novos e-mails
  mailboxes "="
  mailboxes "=Lists"

  # listas de grupos de e-mails (isso são expressões regulares, não são curingas!)
  #subscribe "subscribe-.*@server\\.org"

  # Configuração de envio SMTP (para envio de e-mail)
  #set smtp_url=smtp://MEU-EMAIL@gmail.com/``
```


## Configurações (para ler email Offline)
### Local no qual rezidem as configurações do offlineimap
```
  mkdir -p "${HOME}/.config/mutt"
  touch "${HOME}/.config/mutt/offlineimap"
```
### Comando que sincroniza email
```
  mailsync
```

### Dentro do .muttrc
```
  set mbox_type = Maildir
  set sendmail = "/usr/bin/msmtp -a gmail"
  set folder = "${HOME}/.Mail/Gmail"
```

### Sincroniza o email local com o online
```
  offlineimap
```
Ou
* -c == config file
```
  offlineimap -c "${HOME}/.config/mutt/offlineimap"
```

