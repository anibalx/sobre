# FERRAMENTAS
```sh
  apt install cups printer-driver-gutenprint
```

# CONFIGURAÇÃO DE USUÁRIO
```sh
  usermod -a -G lpadmin <USER>
```

# LOCAL DE CONFIGURAÇÃO
```HTML
  localhost:631
```

# PÓS ADIÇÃO E CONFIGURAÇÃO DA IMPRESSORA
```sh
  service cups restart
```

# NOME DA IMPRESSORA
```sh
  lpstat -p -d
```
