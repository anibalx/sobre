# INFORMAÇÕES
> Dentro do mpv.  
```sh
CTRL+p === gm
```  

# ABRIR MUTADO 
```sh
  mpv --mute=yes <ARQUIVO>
```

# TOCAR RANDÔMICO
```sh
  mpv --shuffle <DIRETÓRIO>
```

# TITLE
```sh
  mpv --title="<TITLE>"
```

# SUB-FILE
```sh
  mpv --sub-file="<SUB-FILE>.srt"
```

# VIDEO IN TERMINAL GNOME-TERMINAL
```sh
  mpv --vo=tct /path/to/your/video.mp4
```

# SELECIONE A PLAYLIST
> Dentro do mpv, vários comandos começam com g-<<letra>>.  
```sh
  gp
```

# MUDAR ÁUDIO
> Dentro do mpv, vários comandos começam com g-<<letra>>.  
```sh
  ga
```  
> OU

```sh
SHIFT+3 === #
```  

# CRIA COMANDO
Em **"#{HOME}/.config/mpv/input.conf"** adicione a seguinte linha:  
```
S playlist-shuffle
```  

## Como Usar
```
SHIFT + s
```  

---

# RHYTHMBOX
```sh
rhythmbox-client --play-uri="file://$(pwd)/Twice - GO HARD [VSc74fDej4I].mp3
```
