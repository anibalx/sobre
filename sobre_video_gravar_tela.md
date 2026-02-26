# Comandos

## Verificar qual é o Servidor Gráfico
```
echo $XDG_SESSION_TYPE
loginctl show-session $(loginctl | grep $(whoami) | awk '{print $1}') -p Type
```  
---

## Descobrir resolução da tela
```bash
xrandr | grep '*'
xdpyinfo | grep dimensions
wlr-randr  # para compositors wlroots
```  

---

## ffmpeg
```
ffmpeg -y -f x11grab -s 1366x768 -i :0.0 out.mkv
ffmpeg -f x11grab -s 1920x1080 -i :0.0 output.mp4
```  

> Gravar tela inteira
```
ffmpeg -f x11grab -i :0.0 -c:v libx264 -preset ultrafast output.mp4
```  

> Gravar com áudio (PulseAudio)
```
ffmpeg -f x11grab -i :0.0 -f pulse -i default -c:v libx264 -c:a aac output.mp4
ffmpeg -f x11grab -s 1920x1080 -i :0.0 \
       -f pulse -i default \
       -c:v libx264 -preset ultrafast -c:a aac output.mp4
```  

> Gravar com taxa de quadros específica
```
ffmpeg -f x11grab -framerate 30 -s 1920x1080 -i :0.0 output.mp4
```  

> Gravar região específica  
```
ffmpeg -f x11grab -s 1920x1080 -i :0.0+100,200 -c:v libx264 output.mp4
ffmpeg -f x11grab -s 800x600 -i :0.0+100,200 output.mp4
```  

> Gravar com cursor  
```
ffmpeg -f x11grab -draw_mouse 1 -i :0.0 output.mp4
ffmpeg -f x11grab -video_size 1920x1080 -framerate 30 -i :0.0 \
       -draw_mouse 1 output.mp4
```  

> Gravar com webcam picture-in-picture  
```
ffmpeg -f x11grab -video_size 1920x1080 -framerate 30 -i :0.0 \
       -f v4l2 -video_size 320x240 -i /dev/video0 \
       -filter_complex "[1:v]scale=320:240[webcam];[0:v][webcam]overlay=main_w-overlay_w-10:10" \
       output.mp4
```  

> Gravação com delay (para streaming)  
```
ffmpeg -f x11grab -video_size 1920x1080 -framerate 30 -i :0.0 \
       -c:v libx264 -preset ultrafast -tune zerolatency \
       -f mpegts udp://localhost:1234
```  

> Gravação segmentada (útil para longas gravações)  
```
ffmpeg -f x11grab -video_size 1920x1080 -framerate 30 -i :0.0 \
       -c:v libx264 -segment_time 3600 -f segment output_%03d.mp4
```  

### ffmpeg com pipewire
> Primeiro, listar as fontes disponíveis  
```
pw-link -o
pw-link -i
```  

> Gravar tela (o nome pode variar)  
```
ffmpeg -f pipewire -i "screen-capture-record" output.mp4
```  

### xdg-desktop-portal (funciona em GNOME/KDE)
> Usando um wrapper como grim/slurp para selecionar área  
```
grim -g "$(slurp)" - | ffmpeg -i pipe:0 output.mp4
```  

---

## wf-recorder
```
wf-recorder -f out.mp4 2>-
```  

> Gravar tela inteira
```
wf-recorder -f output.mp4
```  

> Gravar com codec específico
```
wf-recorder -c h264_vaapi -f output.mp4
```  

> Gravar área específica (geometria)
```
wf-recorder -g "1920x1080+0,0" -f output.mp4
```  

> Gravar com áudio
```
wf-recorder -a -f output.mp4
```  

> Gravar monitor específico
```
wf-recorder -o HDMI-A-1 -f output.mp4
```  

> Gravar com taxa de quadros
```
wf-recorder -r 60 -f output.mp4
```  

> Gravar sem codec de hardware
```
wf-recorder -c libx264 -f output.mp4
```  

> Seleção interativa de área (com slurp)
```
wf-recorder -g "$(slurp)" -f output.mp4
```  

---

# Windows

## ffmpeg
```
ffmpeg -f gdigrab -framerate 10 -i desktop [output]
```  

```
ffmpeg -f gdigrab -framerate ntsc -offset_x 10 -offset_y 20 -video_size 640x480 \
-show_region 1 -i desktop [output]
```  

> Gravar tela inteira
```
ffmpeg -f gdigrab -i desktop -c:v libx264 -preset ultrafast -crf 18 output.mp4
```  

> Gravar tela inteira com áudio
```
ffmpeg -f gdigrab -i desktop -f dshow -i audio="Stereo Mix" -c:v libx264 -c:a aac output.mp4
```  

> Gravar uma janela específica
```
ffmpeg -f gdigrab -i title="Nome da Janela" -c:v libx264 -preset ultrafast output.mp4
```  

> Gravar região específica (x,y offset + largura,altura)
```
ffmpeg -f gdigrab -offset_x 100 -offset_y 100 -video_size 1280x720 -i desktop output.mp4
```  

> Gravar com taxa de quadros específica
```
ffmpeg -f gdigrab -framerate 30 -i desktop -c:v libx264 output.mp4
```  

> Gravar com cursor do mouse visível
```
ffmpeg -f gdigrab -draw_mouse 1 -i desktop output.mp4
```  

---

# REFERÊNCIAS
[A dirty hack to enable acceptable sway wm screen recording - StackOverflow](https://blog.spirotot.com/posts/a-dirty-hack-to-enable-acceptable-sway-wm-screen-recording/)  
[Capture windows screen with ffmpeg - StackOverflow](https://stackoverflow.com/questions/6766333/capture-windows-screen-with-ffmpeg)  
