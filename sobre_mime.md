# COMO DESCOBRIR E MUDAR UM MIMETYPE

## Observação sobre apresentação
Neste arquivo, serão utilizadas formas diferentes de representação do diretório referente ao usuário, em Unix-like.  
De maneira direta, isso não vai mudar os resultados da exxecução dos códigos.  
Serão demonstradas, para que ambas as formas se tornem normalizáveis quando encontradas e exibidas a quem aplicar.  

### Primeira Forma
```sh
  /home/${USER}/
```  

### Segunda Forma
```sh
  ~/
```  

---

## Precedência do usuário em relação ao sistema
As configurações de usuário possuem precedência em relação as do sistema.  

E se encontram em:  
```sh
  /home/${USER}/.config
```  

Já as dos sistema se encontram em:  
```sh
  /etc/
```  

---

## Verificar a existência
Antes de começar o processo, verifique a existência do MimeType em seu sistema.  
Em geral, os sistema irá procurar em:  
```sh
  /home/${USER}/.local/share/applications
```  

OU

```sh
  /usr/share/applications
```  

Esse assunto será retomado mais abaixo.  

---

## Limpar o chache
Caso deseje, remova o cache MIME do usuário e peça o sistema para reconstruí-lo.  
```sh
  rm /home/${USER}/.cache/mimeinfo.cache
  update-desktop-database /home/${USER}/.config/mimeapps.list
```  

---

## Descobre o tipo MIME do arquivo
```
  xdg-mime query filetype arquivo.txt
```  

OU  

> Use o comando `file` com a flag `--mime-type` para identificar o tipo MIME de um arquivo:  
```bash
  file --mime-type nome_do_arquivo
```  

---

## Descobre o aplicativo padrão MIME do arquivo
```
  xdg-mime query default text/plain
```  

### Busca o local no qual se encontra o aplicativo MIME
> **nvim.desktop** = exemplo de aplicação MIME que abre text/plain  
```
   find / nvim.desktop
```  

OU  

```
   fd nvim.desktop /
```  

---

## Exibe os aplicativos MIME
**OBS**: _/usr/share/applications_ = exemplo de local dos MIME  

> Exibe os arquivos dentro do direitório.  
```sh
  ls /usr/share/applications/
```  

> Pega os arquivos **txt** registrados dentro do arquivo MIME.  
```sh
  grep 'txt' /etc/mime.types
```  

---

## Escolher (Definir) APPLICATION MIME
```sh
  xdg-mime default nome_do_aplicativo.desktop tipo/mime
```  

### Exemplo com NeoVim
```sh
  xdg-mime default nvim.desktop text/plain
```  

---

## Exibe novo aplicativo padrão MIME do arquivo
```sh
  xdg-mime query default text/plain
```  

---

## Atualizar a base de dados
```sh
  update-desktop-database ~/.config/mimeapps.list
```  

OU  

> Ambientes Gnome
```sh
  gio mime --update-database ~/.config/mimeapps.list
```  

OU  

> Ambientes KDE Plasma
```sh
  kbuildsycoca5 --no-daemon
```  

OU  

> Ambientes XFCE
```sh
  update-mime-database ~/.config
```  

---

## Abrir arquivo
```sh
xdg-open nome_do_arquivo
```  

---

## Automatização para verificar e abrir tipo específico de arquivo
```sh
#!/usr/bin/env bash
mime_type=$(file --mime-type -b "$1")
case "$mime_type" in
    text/plain) xdg-open "$1" ;;
    image/jpeg) feh "$1" ;;
    *) echo "Tipo MIME não suportado: $mime_type" ;;
esac
```  

---

# REFERÊNCIA
[Brodie Robertson - Linux: How To Change Your Default Applications In XDG MIME](https://www.youtube.com/watch?v=z3F0hTigMvU)  
[XDG-MIME](https://cgit.freedesktop.org/xdg/xdg-utils/tree/scripts/xdg-mime.in)  
[XDG_MIME_Applications](https://wiki.archlinux.org/title/XDG_MIME_Applications)  
[MIME type in Ubuntu](https://askubuntu.com/questions/586476/how-to-assign-set-a-mime-type-to-a-file)  
[FIle mime types](https://www.baeldung.com/linux/file-mime-types)  
[HTPPS MIME Types](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Basics_of_HTTP/MIME_types)  
[XDG MIME Command](https://stackoverflow.com/questions/2060284/how-to-use-the-xdg-mime-command)  
[Easy config XDG](https://unix.stackexchange.com/questions/36380/how-to-properly-and-easy-configure-xdg-open-without-any-environment)  
[Zathura config](https://git.pwmt.org/pwmt/zathura/-/issues/45)  
[Error minor/major XDG-MIME](https://www.google.com/search?q=xdg-mime is not in the form %27minor/major%27)  
