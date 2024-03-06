# Notificação
```
notify-send "Cabeçalho" "<b>Texto</b>" 
```

```
notify-send "Alô mundo" "Cheguei e trouxe o notify" \
	-i gtk-dialog-info
```

```
notify-send "Quer ir ao Google?" \
	"https://google.com"
```


## Avisa o fim de um processo em background
```
cat dispara_job.sh
```

### Programa
```
#!/bin/bash
# Avisa o término ode um job, usando p  notification-send
eval "$1"
```

### Execução do Programa
```
dispara_job.sh 'time find / > /dev/null 2>&1' &
```

### Notificação do programa acima
```
notify-send -i terminal "Acabou" "\nFim do job $1"
```

## Avisa o alerta de temperatura do programa
```
cat AlertaTemp.sh
```

```
#!/bin/bash
acpi -t | while read Lixo Cpu Temp Lixo
do [[ $Temp > 40 ]] && notify-send -u critical "Perigo CPU $Cpu" "Está com $Tempº de febre"
done
```
