# Montagem de sistema
```
    mount /dev/sdb1 /mnt

    mount --bind /dev/  /mnt/dev/
    mount --bind /proc/ /mnt/proc/
    mount --bind /sys/  /mnt/sys/

    chroot /mnt/
```  

# Desmonte de tudo
```
    umount -l /mnt/*
    umount /mnt/
```  

---

# Montagem com arch-chroot

```
    mount /dev/sdb1 /mnt
```  

```
    arch-chroot /mnt/
```  
