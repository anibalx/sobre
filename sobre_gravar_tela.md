# Comandos

## ffmpeg
```
ffmpeg -y -f x11grab -s 1366x768 -i :0.0 out.mkv
```  

```
ffmpeg -f gdigrab -framerate 10 -i desktop [output]
```  

```
ffmpeg -f gdigrab -framerate ntsc -offset_x 10 -offset_y 20 -video_size 640x480 \
-show_region 1 -i desktop [output]
```  

## wf-recorder
```
wf-recorder -f out.mp4 2>-
```  

---

# REFERÊNCIAS
[A dirty hack to enable acceptable sway wm screen recording - StackOverflow](https://blog.spirotot.com/posts/a-dirty-hack-to-enable-acceptable-sway-wm-screen-recording/)  
[Capture windows screen with ffmpeg - StackOverflow](https://stackoverflow.com/questions/6766333/capture-windows-screen-with-ffmpeg)  
