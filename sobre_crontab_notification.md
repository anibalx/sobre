# NOTIFICAÇÃO NA ÁREA DE TRABALHO

## Ferramentas
* [crontab](https://man7.org/linux/man-pages/man5/crontab.5.html) (já instalado)
* [dunstify](https://dunst-project.org/)

## Intalação
**Debian**
```
  apt install dunst
```
**OpenSuse**
```
  zypper in dunst
```
**Fedora**
```
  dnf install dunst
```
## Comandos
Abrir __crontab__
```
  crontab -u "${USER}" -e
```
Comando a ser adcionado
```
  * * * * *  DISPLAY=":0.0" DBUS_SESSION_BUS_ADDRESS='unix:path=/run/user/1000/bus' /usr/bin/dunstify <COLOQUE AQUI SUA MENSAGEM>
```
EX:  
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; A cada três (3) horas, exiba a mensagem.
```
*/60 */3 * * * DISPLAY=":0.0" DBUS_SESSION_BUS_ADDRESS='unix:path=/run/user/1000/bus' /usr/bin/dunstify -t 600000 "TÍTULO" "MENSAGEM" 
```
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Nos dias 18 e 19, das 10:00 da manhã até as 00:00 da noite, de hora em hora (00 minutos), exiba a mensagem.
```
  00 10-00 18-19 1 * DISPLAY=":0.0" DBUS_SESSION_BUS_ADDRESS='unix:path=/run/user/1000/bus' /usr/bin/dunstify -t 900000 "TÍTULO" "MENSAGEM"
```
**OBS**
>"* * * * *"              => padrão de verificação temporal que segue o cron  
>DISPLAY=":0.0"           => exibe a notificação na tela principal  
>DBUS_SESSION_BUS_ADDRESS => recebe o caminho do sistema de arquivos temporário (/run) para onde deve ser apontado

# REFERÊNCIAS
[Dunstify in crontab](https://gitmemory.com/issue/dunst-project/dunst/634/497375737)  
[Unable to send notifications from cron job](https://unix.stackexchange.com/questions/560724/unable-to-send-notifications-from-cron-job)  
[Cron with notify-send](https://stackoverflow.com/questions/16519673/cron-with-notify-send)  
[Diferenças entre /run e /var/run](https://qastack.com.br/unix/175345/difference-between-run-and-var-run)
