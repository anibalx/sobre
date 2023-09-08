# LOCAL DAS PARTIÇÔES
```
  /proc/partitions
```

# EXIBA TODOS OS FILEFSYSTEM MOUNTADOS
```
  findmnt
```

# PEGA O LABEL
```
  blkid -o export | grep LABEL | cut -f2 -d=
```

```
  blkid -s LABEL
```

```
  lsblk -o LABEL
```

# PEGA O DEVICE
```
  blkid -o device
```

# FERRAMENTAS PARA MONTAGEM
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

# MOUNT WITH NAME
## Mount
```
  mount -L label_name_here /path/to/mount/point
```
## Udisksctl
```
  udisksctl mount -b device_name
```

# UMOUNT WITH NAME
## Umount
```
  umount -L label_name_here /path/to/mount/point
```
## Udisksctl
```
  udisksctl umount -b device_name
```

# REFERÊNCIAS
[set label name - Tecmint](https://www.tecmint.com/change-modify-linux-disk-partition-label-names/)
[Mount Partition with Label Names - Cyberciti](https://www.cyberciti.biz/faq/rhel-centos-debian-fedora-mount-partition-label/)
[Auto-Mount Point With udisksctl - askUbuntu](https://askubuntu.com/questions/342188/how-to-auto-mount-from-command-line)
