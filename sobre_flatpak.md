## Instala aplicação
```sh
flatpak install <APP>
flatpak install gimp
```  

## Desinstala aplicação instalada
```sh
flatpak uninstall <ID_APP>
flatpak uninstall org.gimp.GIMP
```  

## Executa aplicação instalada
```sh
flatpak run <ID_APP>
flatpak run org.gimp.GIMP
```  

## Lista apenas aplicações instaladas
```sh
flatpak list --app
```  

## Atualiza aplicações instaladas
```sh
flatpak update
```  

## Reparar de aplicações instaladas localmente
```sh
flatpak repair
```  

## Histórico de mudanças na instalaçao local do Flatpak
```sh
flatpak repair
```  

## Redefinir permissões de aplicações instaladas
```sh
flatpak permission-reset <ID_APP>
flatpak permission-reset org.gimp.GIMP
```  

## Nome e tamanho dos pacotes flatpak
```sh
flatpak --columns=name,size list
```  

## Tipos de instalação, tamanho e ID
```sh
flatpak --columns=app,name,size,installation list
```  

## Flatpak instalado pelo usuário
```sh
flatpak --columns=name,size --user list
```  

## Desinstale os não utilizados
```sh
flatpak uninstall --unused
```  

## Desinstale todos os flatpak
```sh
flatpak uninstall --all
```  

## Limpe o cache
```sh
sudo rm -rfv /var/tmp/flatpak-cache-*
```  

---

# REFERÊNCIAS
[Flatpak.org](https://flatpak.org/)  
[Flatpak Docs](https://docs.flatpak.org/en/latest/getting-started.html)  
[How to Clean Up Flatpak Apps to Clear Disk Spac](https://www.debugpoint.com/clean-up-flatpak/)  
