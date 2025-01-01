# Manual
```
  man mount.fuse
```  

---

# Disposivos montados
```
  /etc/mtab
  /proc/mounts
  /proc/self/mountinfo
```  

## ou ainda
```  
  /proc/bus/input/devices
```  

## ou ainda
```
  /proc/devices
```  

## ou ainda com utilitários do sistema
* -m, --mtab             pesquisa na tabela de sistemas de arquivos montados (inclui opções de espaço de usuário)
* --kernel		 pesquisa na tabela do kernel de sistemas de arquivos
* -a, --all              desabilita todos os filtros embarcados, exibe todos os sistemas de arquivo
```
  findmnt
  findmnt -m
  findmnt --kernel
  findmnt -a
```  

## ou ainda
```
  lsblk
```  

## ou ainda
```
  blkid
```  

---

# Informaçõs sobre os dispositivos (devices)
```
  usb-devices
  /sys/kernel/debug/usb/devices
```

---

# Lista os dispositivos (devices) USB
```
  lsusb
```

---

# Lista os dispositivos (devices) PCI
```
  lspci
  /usr/share/pci.ids
```
## ou ainda
```
  /proc/bus/pci/devices
```
