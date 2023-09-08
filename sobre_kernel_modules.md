# Mostra o status dos módulos
```
  lsmod
  /proc/modules
```

---

# Firmware
Rodo no processador do pŕoprio dispositivo 
(não no processador principal da máquina - onde roda o kernel)
## MODINFO
Permite averiguar as informações sobre o módulo que roda 
no processador do dispositivo disponibilizado pelo provedor
```
  modinfo firm.fw
```

---

# LSPCI
**Barramento PCI** uma placa de rede, por exemplo

* mostra as caracteristicas do módulo/driver (dispositivo) 
do tipo ethernet, onde são usados cabos de rede
* -nn = mostra os nomes e números do ID dos dispositivos
* -k  = drivers do kernel
* -d  = mostra os dispositivos específicos
```
  lspci -nnkd::0200
```

* mostra as caracteristicas do módulo/driver (dispositivo) WiFi
* -nn = mostra os nomes e números do ID dos dispositivos
* -k  = drivers do kernel
* -d  = mostra os dispositivos específicos
```
  lspci -nnkd::0280
```

---

# LSUSB
**Barramento USB** uma placa de rede, por exemplo

* mostra as caracteristicas do módulo/driver (dispositivo) 
do tipo ethernet, onde são usados cabos de rede
* -t = mostra a árvore de hierarquia dos dispositivos usb físicos
* -v = verbose
```
  lsusb -tv
```
