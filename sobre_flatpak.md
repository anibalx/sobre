
## Nome e tamanho dos pacotes flatpak
```
flatpak --columns=name,size list
```

## Tipos de instalação, tamanho e ID
```
flatpak --columns=app,name,size,installation list
```

## Flatpak instalado pelo usuário
```
flatpak --columns=name,size --user list
```

## Desinstale os não utilizados
```
flatpak uninstall --unused
```

## Desinstale todos os flatpak
```
flatpak uninstall --all
```
## Limpe o cache
```
sudo rm -rfv /var/tmp/flatpak-cache-*
```

# REFERÊNCIAS
[How to Clean Up Flatpak Apps to Clear Disk Spac](https://www.debugpoint.com/clean-up-flatpak/)
