# Keys
```
o (minúsculo) = edita teclas
M (maiúsculo) = abre browser externo
H (maiúsculo) = mapa de teclas (keymap)
```  

# Dado que foi configurado algum comando:
## Ex1: definição de um "External Browser"
> Permite que um link (URL) seja copiado para a área de tranferência	
```
extbrowser2 sh -c 'printf %s "$0" | xsel'
```  

### Para fazer funcionar
Cursor sobre o link, aperte:  
> Salva na área de tranferência
> Abre o link num navgador externo
```
2 ESC M (maiúsculo)
ESC M (maiúsculo)
```  

# Ex2: definição de um "External Browser"
```
extbrowser3 mpv -ytdl --vo=opengl --ao=alsa <- permite que o vídeo possa ser assistido através do link (URL) sem um browser externo	
```  

## Para fazer funcionar: 
Cursor sobre o link, aperte:  
```
3 ESC M (maiúsculo) <- salva na área de tranferência
ESC M (maiúsculo)	<- abre o link num navgador externo
```  

```
ctrl + b (C-b) = volta para o local anterior
ctrl + o (C-o) = abre um editor externo
```  

---

# REFERÊNCIAS
[Abrir URLS dentro do Lynx](https://www.reddit.com/r/commandline/comments/4mgxps/how_to_use_vlc_to_open_youtube_urls_in_lynx/)  
[W3M Keymap](https://github.com/tokuhirom/w3m/blob/master/doc-jp/keymap.default)  
[](https://www.youtube.com/watch?v=QczYT67JqYs)  
[URL no W3M](https://unix.stackexchange.com/questions/12497/yanking-urls-in-w3m)  
[W3M com o MPV](https://www.reddit.com/r/commandline/comments/6ixptv/open_current_w3m_video_site_url_with_mpv_the_easy/)  

[Use VLC com W3M](https://francismurillo.github.io/2017-01-11-Using-vlc-With-w3m/)  
[VLC com Lua](https://github.com/videolan/vlc/blob/master/share/lua/playlist/youtube.lua)  
[Forum Videolan](https://forum.videolan.org/viewtopic.php?t=146560)  
[GitHub VLC](https://github.com/videolan/vlc/blob/master/share/lua/playlist/youtube.lua)  
