# OPÇÕES
  * -e = Execute (um comando)
  * -r = Recursivo
  * -v = Verbose: modo detalhado
  * -a = Arquivamento: preserva links, datas etc. (não pode ser usado com -r)
  * -h = Mostra uma saída legível para humanos
  * -z = Comprimir dados enquanto em tráfego
  * --delete = Deletar (sincroniza totalmente, se não houver o arquivo no fonte, não haverá no destino)


## Ex1
Conexão em uma porta ssh diferente (-e), 
recursivamente (-r) 
em modo verboso (-v), que exibe informações
```
  rsync -ver 'ssh -p 2806' <LOCAL_DIR>/ <USER_SERVER>@<IP_SERVER>:<SERVER_DIR>
```


## EX2
Preserve os arquivos - links, permissões, datas etc. - (-a) e 
enquanto forem enviados, comprima-os (-z). 
Tudo isso em modo verboso (-v) e 
de modo que humanos (-h) consigam ler
```
  rsync -vahz <LOCAL_DIR>/ <LOCAL_DIR>/ <USER_SERVER>@<IP_SERVER>:<SERVER_DIR>
```

## Ex3
Preserve os arquivos - links, permissões, datas etc. - (-a) e 
enquanto forem enviados, comprima-os (-z). 
Tudo isso em modo verboso (-v) e 
de modo que humanos (-h) consigam ler
Contudo, exclua todos os arquivos (*.<EXTENSION>) 
de um tipo específico de um determinado diretório (--exclude=<LOCAL_DIR>/*.<EXTENSION>)
```
  rsync -vahz --exclude=<LOCAL_DIR>/*.<EXTENSION> <LOCAL_DIR>/ <LOCAL_DIR>/ <USER_SERVER>@<IP_SERVER>:<SERVER_DIR>
```


## Ex4
Preserve os arquivos - links, permissões, datas etc. - (-a) e 
enquanto forem enviados, comprima-os (-z). 
Tudo isso em modo verboso (-v) e 
de modo que humanos (-h) consigam ler
Contudo, exclua todos os arquivos (*.<EXTENSION>) 
de um tipo específico de um determinado diretório (--exclude=<LOCAL_DIR>/*.<EXTENSION>)
Só que desta vez, não envie apenas os arquivos, mas sim o diretório contendo os arquivos (<LOCAL_DIR> <- sem barra no final)
```
  rsync -vahz --exclude=<LOCAL_DIR>/*.<EXTENSION> <LOCAL_DIR> <LOCAL_DIR> <USER_SERVER>@<IP_SERVER>:<SERVER_DIR>
```


## Ex5
Preserve os arquivos - links, permissões, datas etc. - (-a) e 
enquanto forem enviados, comprima-os (-z). 
Tudo isso em modo verboso (-v) e 
de modo que humanos (-h) consigam ler
Contudo, exclua todos os arquivos (*.<EXTENSION>) 
de um tipo específico de um determinado diretório (--exclude=<LOCAL_DIR>/*.<EXTENSION>)
Só que desta vez, não envie apenas os arquivos, mas sim o diretório contendo os arquivos (<LOCAL_DIR> <- sem barra no final)
Além disso, sincronize os arquivo que existirem e não existirem mais (--delete)
```
  rsync -vahz --delete --exclude=<LOCAL_DIR>/*.<EXTENSION> <LOCAL_DIR> <LOCAL_DIR> <USER_SERVER>@<IP_SERVER>:<SERVER_DIR>
```


## Ex6
Do servidor, envie para armazenamento local.
```
  rsync <USER_SERVER>@<IP_SERVER>:<SERVER_DIR> <LOCAL_DIR>/
```
