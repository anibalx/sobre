 # COMO DESCOBRIR E MUDAR UM MIMETYPE
 
 ## Descobre o tipo MIME do arquivo
 ```
   xdg-mime query filetype arquivo.txt
 ```
 ## Descobre o aplicativo padrão MIME do arquivo
 ```
   xdg-mime query default text/plain
 ```
 ### Busca o local no qual se encontra o aplicativo MIME
 **nvim.desktop** = exemplo de aplicação MIME que abre text/plain
 ```
    find / nvim.desktop
 ```
 ou
 ```
    fd nvim.desktop /
 ```
 ## Exibe os aplicativos MIME
 **OBS**: _/usr/share/applications_ = exemplo de local dos MIME
 ```
   ls /usr/share/applications/
 ```
 ```
   grep 'txt' /etc/mime.types
 ```
 ## Escolher APPLICATION MIME
 ```
   xdg-mime default nvim.desktop text/plain
 ```
 ## Exibe novo aplicativo padrão MIME do arquivo
 ```
   xdg-mime query default text/plain
 ```
 
 # REFERÊNCIA
 >[Brodie Robertson - Linux: How To Change Your Default Applications In XDG MIME](https://www.youtube.com/watch?v=z3F0hTigMvU)
 >[XDG-MIME](https://cgit.freedesktop.org/xdg/xdg-utils/tree/scripts/xdg-mime.in)  
 >[XDG_MIME_Applications](https://wiki.archlinux.org/title/XDG_MIME_Applications)  
 >[MIME type in Ubuntu](https://askubuntu.com/questions/586476/how-to-assign-set-a-mime-type-to-a-file)  
 >[FIle mime types](https://www.baeldung.com/linux/file-mime-types)  
 >[HTPPS MIME Types](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Basics_of_HTTP/MIME_types)  
 >[XDG MIME Command](https://stackoverflow.com/questions/2060284/how-to-use-the-xdg-mime-command)  
 >[Easy config XDG](https://unix.stackexchange.com/questions/36380/how-to-properly-and-easy-configure-xdg-open-without-any-environment)  
 >[Zathura config](https://git.pwmt.org/pwmt/zathura/-/issues/45)  
 >[Error minor/major XDG-MIME](https://www.google.com/search?q=xdg-mime is not in the form %27minor/major%27)
