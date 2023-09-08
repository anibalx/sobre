# Sudo in OpenSuse
## 1ª opção
Dentro do arquivo sudoer.s, comente a seguinte linha:
```
    Defaults targetpw   # ask for the password of the target user i.e. root
```

Agora, ela deve ficar parecida como abaixo:
```
    ## Defaults targetpw   # ask for the password of the target user i.e. root
```

## 2ª opção
Ou então, insira a linha abaixo (onde estiver <MY_USER>, insira seu nome de usuário):
```
    <MY_USER>  ALL=NOPASSWD:   /usr/bin/zypper refresh, /usr/bin/zypper update
```

# Sudo Explicação
- %       == todos os usuários
* ALL     == qualquer comando
* ALL:ALL == de qualquer lugar 
* ALL     == a qualquer momento
```
  # Allow members of group sudo to execute any command
  %sudo ALL=(ALL:ALL) ALL
```

# REFERÊNCIAS
[Suse support](https://www.suse.com/support/kb/doc/?id=000016906)
