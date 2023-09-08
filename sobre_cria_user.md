# SheeBang
```sh
  !/usr/bin/env bash
```

# Cria usuário
```sh
  useradd <USER>
```

# Seta password
```sh
  passwd <USER>
```

# Cria usuário com home
* -m
* --create-home
```sh
  useradd -m <USER>
```

# Cria usuário com home específico
* -d
* --home
```sh
  useradd -m -d /opt/<USER> <USER>
```

# Cria usuário com id específico
* -u
* --uid
```sh
  useradd -u 1000 <USER>
```

# Cria usuário com gid específico
* -g
* --gid
```sh
  useradd -g users <USER>
```

# Verifica o id
```sh
  id -gn <USER>
```

# Cria usuário com gid específico
* -G
* --groups
```sh
  useradd -g users -G wheel,developepers <USER>
```

# Cria usuário com shell específico
* -s
* --shell
```sh
  useradd -s /usr/bin/zsh <USER>
```


# Cria usuário com comentário customizado
* -c
* --comment
```sh
  useradd -c "Test User Account" <USER>
```


# Cria usuário com data de expiração
* -c
* --expiredate
```sh
  useradd -e 2022-02-28 <USER>
```

# Cria usuário sistema
* -r
* --system
```sh
  useradd -r <USER>
```

# Seta valores padrões do usuário
* -D
* --defaults
```sh
  useradd -D
  useradd -D -s /usr/bin/bash
```

# Deleção e criação de usuário
```sh
  userdel --force --remove $USER
  useradd --gid users --shell /usr/bin/bash --create-home rui
  cp --recursive my_config/ /home/$USER
  chown --recursive $USER /home/$USER/my_config
  chgrp --recursive users /home/$USER/my_config
  passwd $USER
```

# REFERÊNCIAS
[Linuxsize - Create Users](https://linuxize.com/post/how-to-create-users-in-linux-using-the-useradd-command/)
