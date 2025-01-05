# LOCAL DAS PARTIÇÔES
```
  /proc/partitions
```  

---

# EXIBA TODOS OS FILEFSYSTEM MOUNTADOS
## Ou com findmnt
```
  findmnt
```  

## Ou com lsblk
```
  lsblk
```    

## Ou com blkid
```
  blkid
```  

---

# PEGA O DEVICE
```
  blkid -o device
```  

# PEGA O LABEL
* -f<LIST>, --fields <LIST>		    = selecione a partir de um campo
* -d<DELIMITADOR>, --delimiter<DELIMITADOR> = delimite por algo especificado 
```
  blkid -o export | grep LABEL | cut -f2 -d=
```

```
  blkid -s LABEL
```

```
  lsblk -o LABEL
```  

---

# FERRAMENTAS PARA ADICIONAR UM LABEL
## EXT2 EXT3 EXT4
```
  e2label /dev/sda1 ROOT
```

```
  tune2fs –L ROOT_PART /dev/sda1
```  

## NTFS
```
  ntfslabel /dev/sda5 NTFS_DIR
```  

## RaiserFS
```
  reiserfstune –l HOME_PART /dev/sdb1
```  

## SWAP
```
  mkswap -L SWAP_PART /dev/sda5
```  

## exFAT
```
  exfatlabel /dev/sda3 EX_PART
```  

## VFAT (EXTENSÃO FAT16)
```
  fatlabel /dev/sda3 EX_PART
```  

---

# MOUNT COM LABEL
## Mount
* -L, --label 		    monte uma partição através de seu respectivo label  
```
  mount -L <LABEL_NAME_HERE> /path/to/mount/point
```  

## Udisksctl
* -b, --block-device        monte o dispositivo (device) pelo bloco
```
  udisksctl mount -b <BLOCK_DEVICE_NAME>
```  

---

# UMOUNT WITH LABEL
## Umount
* -L, --label		    monte uma partição através de seu respectivo label  
```
  umount -L <LABEL_NAME_HERE> /path/to/mount/point
```  

---

## Udisksctl
* -b, --block-device        monte o dispositivo (device) pelo bloco
```
  udisksctl umount -b <BLOCK_DEVICE_NAME>
```  

# REFERÊNCIAS
[set label name - Tecmint](https://www.tecmint.com/change-modify-linux-disk-partition-label-names/)
[Mount Partition with Label Names - Cyberciti](https://www.cyberciti.biz/faq/rhel-centos-debian-fedora-mount-partition-label/)
[Auto-Mount Point With udisksctl - askUbuntu](https://askubuntu.com/questions/342188/how-to-auto-mount-from-command-line)
