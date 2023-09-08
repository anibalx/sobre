# Com FFMPEG
```
                            HH:MM:SS     HH:MM:SS
  ffmpeg -i entrada.mp3 -ss 00:07:11 -to 00:07:12.19697 -c copy saida.mp3
```
# Com AVCONV
```
  avconv -i entrada.m4a  -ss *pos* -t *duration* saida.mp3
```
# Com MENCODER
```
  mencoder -ss 00:30:00 -endpos 00:00:05 -oac pcm -ovc copy entrada -o saida
```

# REFERÊNCIAS
[FFMPEG](https://unix.stackexchange.com/questions/182602/trim-audio-file-using-start-and-stop-times)  
[AVCONV](https://askubuntu.com/questions/49799/cutting-of-audio-files)  
[MENCODER](https://askubuntu.com/questions/59383/extract-part-of-a-video-with-a-one-line-command)

