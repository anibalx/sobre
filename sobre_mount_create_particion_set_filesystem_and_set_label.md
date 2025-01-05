# exFAT  
## Cfdisk
Use a ferramenta que desejar para manipular as partições
```
  cfdisk 
```  

## Mkfs
Use a ferramenta que desejar para "buildar" o sistemas de arquivos
```
  mkfs.ext4 <DEVICE> 
    # ex: mkfs.ext4 /dev/sda8
```  

## E2label
Use a ferramenta que desejar para inserir um label num sistema de arquivos ext
```
  e2label <DEVICE> <LABEL> 
    # ex: e2label /dev/sda8 busy
```  

## Chown
Use a ferramenta que desejar para inserir o dono:grupo do dispositivo e suas profundezas
```
  chown -R <USER>:<GROUP> <LOCAL NO QUAL ESTÀ MONTADO O DEVICE>
    ex: chown -R bonha:1000 /mnt/bonha_device
```  

---  

# VFAT (EXTENSÃO FAT16)
## Cfdisk
Use a ferramenta que desejar para manipular as partições
```
  cfdisk 
```  

## Mkfs
Use a ferramenta que desejar para "buildar" o sistemas de arquivos
```
  mkfs.fat <DEVICE> 
    # ex: mkfs.fat /dev/sda8
```  

## Fatlabel
Use a ferramenta que desejar para inserir um label num sistema de arquivos ext
```
  fatlabel <DEVICE> <LABEL> 
    # ex: fatlabel /dev/sda8 my_pendrive
```  

## Chown
Use a ferramenta que desejar para inserir o dono:grupo do dispositivo e suas profundezas
```
  chown -R <USER>:<GROUP> <LOCAL NO QUAL ESTÀ MONTADO O DEVICE>
    ex: chown -R bonha:1000 /mnt/my_pendrive
```  
