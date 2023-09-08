# SUBSTITUA O COMANDO CAT
```sh
  printf "$(< ARQUIVO.EXTENSÂO_DO_ARQUIVO)"
```

# FAÇA UMA FUNÇÂO DISSO
```sh
  func() { printf "$(< $1)" }
```

# ADICIONE AO ALIAS
```sh
  echo " alias cat='func() { printf \"\$(< \$1)\" }' " >> ~/.alias
```

# OU ADICIONE AO RC
```sh
  echo "cat() { printf \"\$(< \$1)\" }" >> ~/.zshrc
  echo "cat() { printf \"\$(< \$1)\" }" >> ~/.bashrc
```

```sh
  echo 'cat() { printf "$(< $1)" }' >> ~/.zshrc
  echo 'cat() { printf "$(< $1)" }' >> ~/.bashrc
```
