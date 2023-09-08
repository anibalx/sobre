# Comportamento do zypper
```
  /etc/zypp/zypp.conf
```

# Cache do zypper
```
  /var/cache/zypp/raw/
```

# Repositórios do Zypper
```
  /etc/zypp/repos.d/
```

# Repositórios customizados (variables)
```
  /etc/zypp/vars.d
```

# Logs do Zypper
```
 /var/log/zypper.log
```

# Logs do YAST
```
 /var/log/YaST2/y2log
```

---

# Instalação do Packaman
* -c = testa URI/URL
* -f = habilita atualização automática do repositório
* -p = define a prioridade do repositório
```
  zypper ar -cfp 90 http://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Tumbleweed/ packman
```

# Deixe o Zypper saber que deseja baixar do Packman
* dup                   = atualiza distribuição
* --from                = do repositório <NAME>
* --allow-vendor-change = dup foca apenas em <NAME>
```
  zypper dup --from packman --allow-vendor-change
```

---

# Log do Zypper
```
  zypper-log
```

# Atualiza distro
```
  zypper dup
```

# Atualiza pacotes
```
  zypper up
  zypper update
   
  zypper up -D
  zypper up --dry-run
```

# Instalação de pacotes
```
  zypper in
  zypper install \!<PACKAGE_NAME>
  zypper install --no-recommends <PACKAGE_NAME> # não instala recomendações
   
  zypper in --details
    
  zypper in -D
  zypper in --dry-run
   
  zypper in -y
  zypper in --no-confirm
   
  zypper in --force-resolution
   
  zypper in -R
  zypper in --no-force-resolution
   
  zypper in --recommends
  zypper in --no-force-resolution
   
  zypper in -d
  zypper in --download-only # instala e depois baixa o pacote
   
  zypper in --download-in-advance # baixa o pacote e depis instala
```

# Pesquisa pacotes
```
  zypper se
  zypper search

  zypper se -d
  zypper se --search-descriptions

  zypper se -s
  zypper se --details
  zypper se -v
  zypper se --verbose

  zypper se -i
  zypper se --installed-only

  zypper se -u
  zypper se --not-installed-only

  zypper se --sort-by-name
  zypper se --sort-by-repo
```

## Saída
```
i+
    installed by user request

i
    installed automatically (by the resolver, see section Automatically installed packages)

v
    a different version is installed

empty
    neither of the above cases

!
    a patch in needed state

.l
    is shown in the 2nd column if the item is locked (see section Package Locks Management)

.P
    is shown in the 2nd column if the item is part of a PTF (A program temporary fix which must be explicitly
    selected and will otherwise not be considered in dependency resolution).

.R
                   is shown in the 2nd column if the item has been retracted (see patch in section Package Types)
```

# Lista pacotes que forneçam o recurso especificado
```
  zypper wp
  zypper search --provides --match-exact
```

# Exibe informações sobre um pacote
```
  zypper info
   
  zypper info -r
  zypper info --repo
   
  zypper info -t
  zypper info --type
   
  zypper info --provides
  zypper info --requires
  zypper info --conflicts
  zypper info --obsoletes
  zypper info --recommends
  zypper info --suggests
  zypper info --supplements
```

# Pacotes padrão de algum repositório
```
  zypper pt
  zypper patterns
  zypper search -s -t pattern
```

# Liste reposítórios
```
  zypper lr
  zypper repos

  zypper lr -pu # lista repositórios em ordem de prioridade
```

# Adiciona reposítório
```
  zypper ar
  zypper addrepo
```

# Renomeie reposítório
```
  zypper nr
  zypper renamerepo
```

# Modifique reposítório
```
  zypper mr
  zypper modifyrepo
```

# Remove reposítório
```
  zypper rr
  zypper removerepo
```

# Instala o código fonte de um pacote
```
  zypper si
  zypper source-install
```

# Vefique as depedências dos pacotes
```
  zypper ve
  zypper verify
   
  zypper ve -D
  zypper ve --dry-run
```

# Lista as atualizações
```
  zypper lu
  zypper list-updates
```

# Purga kernels
```
  zypper purge-kernels
  zypper purge-kernels --details
```

# Remove pacotes
```
  zypper rm
  zypper remove

  zypper remove -u
  zypper remove --clean-deps
   
  zypper remove -U
  zypper remove --no-clean-deps
```
