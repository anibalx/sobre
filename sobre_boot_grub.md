# Boot da máquina

## Dado que esteja no console do grub
```
    grub>
```  

## Mostre os discos
```
    ls
```  

## Mostre um disco
```
    ls (hd0,msdos1)/
```  
* hd0 -> disco
* msdos1 -> partição

## Mostre o nome do host
```
    cat (hd0,msdos1)/etc/hostname
```  

## Carregue o Kernel
```
    linux (hd0,msdos1)/boot/<KERNEL_VERISON>
    linux (hd0,msdos1)/boot/vmlinuz-5.18.11-1-amd64
```  

## Carregue o Disco Inicial
```
    initrd (hd0,msdos1)/boot/<INIT_RD_NAME>
    initrd (hd0,msdos1)/boot/initrd-5.18.11-1-default
```  

## Dê o boot
```
    boot
```  

## Mostre as partições
```
    cat /proc/partitions
```  

## Caso não exita, crie /root
```
    mkdir -p /root
```  

## Monte o "barra" root
```
    mount -t <FILE_SYSTEM_TYPE> -o noatime,nodiratime <DISK_NAME> <DIR_NAME>
    mount -t ext4 -o noatime,nodiratime /dev/sda2 /root
```  
* noatime = Não atualize os tempos de acesso inode neste sistema de arquivos (por exemplo, para acesso mais rápido no carretel de notícias para acelerar servidores de notícias). Isso funciona para todos os tipos de inode (diretórios também), por isso implica nodiratime.
* nodiratime = Não atualize os tempos de acesso do diretório inode neste sistema de arquivos. (Esta opção é implícita quando o noatime é definido.)

## Saia do grub
```
    exit
```  

---

# Caiu no Initramfs
## Dado que esteja no initramfs
```
    (initramfs)
```  

## Veja a partição
```
    lsblk || blkid
```  
* lsblk -> list block
* blkid -> block id

## Exiba os erros
```
    fsck /dev/<DEVICE>
    fsck /dev/sda2
```  

# REFERÊNCIAS
[Boot Rawdisk - a partir de um disco existente](salsa.debian.org/kretcheu/tutoriais/-/blob/master/boot.rawdisk.md)
