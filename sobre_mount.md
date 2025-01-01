# MONTAGEM
## DIRETÓRIOS 
 
* Possible diretory for installation 
	* /tmp/<DIRETORY>
	* /media/{$USER}/<DIRETORY>

In example, manual mount, i create directory in: /tmp/<DIRECTORY>
> mkdir -p	= create directory with not exists
```
  sudo mkdir -p /tmp/arquivos
```  

## MOUNT COMMAND
```
  mount /path/to/mount/point
```  

## UMOUNT COMMAND
```
  umount /path/to/mount/point
```  

## UDISKSCTL COMMAND FOR MOUNT
* -b, --block-device        monte o dispositivo (device) pelo bloco
```
  udisksctl mount -b <BLOCK_DEVICE_NAME>
```  

## UDISKSCTL COMMAND FOR UMOUNT
* -b, --block-device        monte o dispositivo (device) pelo bloco
```
  udisksctl umount -b <BLOCK_DEVICE_NAME>
```  

---

# USB

  * Device -> /dev/<DEVICE>

```
  lsblk
```  

  * possible -> sdc

  * n = number

```
  mount /dev/sdcn /mnt/arquivos
  umount /mnt/arquivos
```  

---

# Smartphone
## Simple-mtpfs
> list device
```
  lsusb
  simple-mtpfs -l
```  

  > n = number

> mount/umount device
```
  simple-mtpfs --device n /tmp/arquivos
  fusermount -u /tmp/arquivos
```  

## Jmtpfs
> list device
```
  jmtpfs -l
```  

> mount/umount device
```
  jmtpfs /tmp/arquivos
  fusermount -u /tmp/arquivos
```  

---

# ISO
```
    mount -o ro -t iso9660 <FILE>.iso /mnt/arquivos
```  


# Pendrive
```
    mount -t vfat /dev/sdc1 /run/media/{$USER}/pendrive
```  

---

# REFERÊNCIAS
[Luke Smith - How to Mount Android Phones in Linux](https://youtube.com/watch?v=lcmJg4OfKzs)
[Como restaurar seu Galaxy aos padrões de fábrica (Hard Reset)](https://www.youtube.com/watch?v=hg5S3VS5oyo)
[Como Funciona o Boot de um Linux？ ｜ O que tem num LiveCD？](https://www.youtube.com/watch?v=5F6BbhgvFOE].webm)
