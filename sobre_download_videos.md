# BUSCAR LINK
* Na página onde se localiza o vídeo, abra as ***_Ferramentas_ _do_ _Desenvolvedor_***  
```
  CTRL + SHIFT + I
        OU
       F12
```  
* Vá para a guia ***_Network_ (_redes_)*** e ***recarregue*** a página.  
* Pequise o nome dos arquivos e localize o ***PRIMEIRO*** pedido ***.m3u8*** extensão, pode ser algo como: ***playlist.m3u8***  

* Abra a solicitação e, na subseção ***_Cabeçalhos_***, você verá o URL completo da solicitação no campo URL da solicitação . Copie-o.

---

# FFMEPG
```
 ffmpeg -i "<input.m3u8>" -c copy -bsf:a aac_adtstoasc "output.mp4" 
```  
## FFMEPG (ONE Drive)
```
  ffmpeg -i "input.mxf" -pix_fmt yuv420p -c:v libx264 -preset fast -crf 22 -c:a aac -b:a 192k -movflags +faststart "test.mp4"
```

---

# YOUTUBE-DL
```
  youtube-dl <input.m3u8>
```  

---

# WISTIA

## Ferramentas de Desenvolvedor
Inspecionar elementos da página procurar por: embed/iframe abrir link encontrado numa nova página.  

## Dentro da nova página
```
Ferramentas de desenvolvedor
Sources
  embed/iframe
    procurar por mp4
      url ... .bin
abrir link numa nova página
```  

## Dentro da nova página
```
  substituir .bin por .mp4
    faça download
```  

---

# REFERÊNCIAS
[FFMPEG mp4 from http live streaming m3u8 file?](https://stackoverflow.com/questions/32528595/ffmpeg-mp4-from-http-live-streaming-m3u8-file)
[Como fazemos o download de um vídeo de URL de blob](https://qastack.com.br/programming/42901941/how-do-we-download-a-blob-url-video)  
[How do we download a blob url video](https://stackoverflow.com/questions/42901942/how-do-we-download-a-blob-url-video)  
[Como baixar vídeo com URL de blob?](https://qastack.com.br/superuser/1033563/how-to-download-video-with-blob-url)  
[How to Use FFmpeg to Download M3U8 File?](https://www.leawo.org/tutorial/how-to-use-ffmpeg-to-download-m3u8-file-1395.html)  
[How to download .m3u8 in once time](https://stackoverflow.com/questions/47233304/how-to-download-m3u8-in-once-time)
