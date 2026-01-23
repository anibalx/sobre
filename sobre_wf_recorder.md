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
