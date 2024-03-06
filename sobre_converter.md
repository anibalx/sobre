```
   ffmpeg -i video.mp4 music.mp3
```

```
   ffmpeg -i video.mp4 -b:a 192K -vn music.mp3
```


# Exemplo
```
FILE="the-file-you-want-to-process.webm";

ffmpeg -i "${FILE}" -vn -ab 128k -ar 44100 -y "${FILE%.webm}.mp3";
```

```
for FILE in *.webm; do
    echo -e "Processing video '\e[32m$FILE\e[0m'";
    ffmpeg -i "${FILE}" -vn -ab 128k -ar 44100 -y "${FILE%.webm}.mp3";
done;
```

```
find . -type f -iname "*.webm" -exec bash -c 'FILE="$1"; ffmpeg -i "${FILE}" -vn -ab 128k -ar 44100 -y "${FILE%.webm}.mp3";' _ '{}' \;
```

# REFERÊNCIAS
[ffmpeg: Extract audio from .WEBM to .MP3](https://bytefreaks.net/gnulinux/bash/ffmpeg-extract-audio-from-webm-to-mp3)


# REFERÊNCIAS
[FFMPEG](https://superuser.com/questions/332347/how-can-i-convert-mp4-video-to-mp3-audio-with-ffmpeg/354662)  

