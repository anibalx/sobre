# Instalação
```
    apt install rkhunter
```

# Log do RK Hunter
```
    /var/log/rkhunter.log
```

# Atualização de mirros
```
    UPDATE_MIRRORS=0
    MIRRORS_MODE=1
```

```
    UPDATE_MIRRORS=1
    MIRRORS_MODE=0
```

```
    WEB_CMD="/bin/false"
```

```
    WEB_CMD="/bin/false"
    WEB_CMD=""
```

# Atualização do RK Hunter
```
    rkhunter --update
```


# Criação de DB local
```
    rkhunter --propupd
```

# Checagem dos arquivos
```
    rkhunter -c
    rkhunter --check
    rkhunter --check --rwo  # mostre, apenas, quando houver modificação
```

# Configure o CRON
## Busca dentro do less
```
    CRON_DAILY_RUN="true"
    CRON_DB_UPDATE="true"
    DB_UPDATE_EMAIL="true"
    REPORT_EMAIL="root"
```

---

# Falso positivo
```
    less /var/log/rkhunter.log
```

## Busca dentro do less
```
    /Warning
```

## Resposta
```
    Warning: The command "/usr/bin/lwp-request" has been replaced by a script: /usr/bin/lwp-request: Perl script text executable
```
> o comando foi substituido por um script: um binário em um lugar, aponta para um script em outro lugar

## Adição a whitelist

### Busca dentro do less
```
    /SCRIPTWHITELIST
```

### Adicione a whitelist
```
    SCRIPTWHITELIST=/usr/bin/lwp-request
```

---

# Teste de email
```
    mail -s "TÍTULO" <EMAIL> <<< "Mensagem"
```

# Verifique o email
```
    email
```

---

# Adição ao Cron
```
    00 05 * * * /usr/bin/rkhunter --cronjob --update --quiet
```
> Todos os dias às 5 da manhã
