# Pacote
```
  ntfs-3g
```
# USO
```
  cfdisk /dev/sdx
```
# Criar NTFS
```
  mkfs.ntfs -f /dev/sdxn
```
# Montagem
```
  mount /dev/sdxn /mnt/myNtfsDir
```
```
  mount -t ntfs /dev/sdxn /mnt/myNtfsDir
```
# REFERÊNCIAS
[fdisk create ntfs](https://unix.stackexchange.com/questions/252625/how-can-i-use-fdisk-to-create-a-ntfs-partition-on-dev-sdx)
