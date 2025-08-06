# Com FFMPEG
```
                            HH:MM:SS     HH:MM:SS
  ffmpeg -i entrada.mp3 -ss 00:07:11 -to 00:07:12.19697 -c copy saida.mp3
```  

```
  ffcut(){
      # ffcut video.mp4 1:47:58 1:51:33
      FILE="${1}"
      EXTENSION="${1##*.}" # Corta qualquer coisa do início, até o último ponto: agua.webm.nim -> .nim
      FILE_NEW="${FILE/.*/_.${EXTENSION}}"
      TIME_0="${2}"
      TIME_1="${3}"
      ffmpeg -i "${FILE}" -ss "${TIME_0}" -to "${TIME_1}" -c copy "${FILE_NEW}"
  }
```  

## Exemplo com a função ffcut

> O exemplo abaixo constroe e executa a função em uma linha  

```
  ffcut(){ FILE="${1}" ; EXTENSION="${1##*.}" ; FILE_NEW="${FILE/.*/_.${EXTENSION}}" ; TIME_0="${2}" ; TIME_1="${3}" ; ffmpeg -i "${FILE}" -ss "${TIME_0}" -to "${TIME_1}" -c copy "${FILE_NEW}"; } ; ffcut video_cut.mp4 1:47:58 1:51:33
```  

---

# Com AVCONV
```
  avconv -i entrada.m4a  -ss *pos* -t *duration* saida.mp3
```  

---

# Com MENCODER
```
  mencoder -ss 00:30:00 -endpos 00:00:05 -oac pcm -ovc copy entrada -o saida
```  

---

# REFERÊNCIAS
[FFMPEG](https://unix.stackexchange.com/questions/182602/trim-audio-file-using-start-and-stop-times)  
[AVCONV](https://askubuntu.com/questions/49799/cutting-of-audio-files)  
[MENCODER](https://askubuntu.com/questions/59383/extract-part-of-a-video-with-a-one-line-command)  
