## Comandos básicos

**df** - Mostra espaço usado e disponível em sistemas de arquivos montados:
```bash
df -h  # formato legível (MB, GB, etc)
df -h /dev/sda1  # informações de uma partição específica
```

**lsblk** - Lista todos os dispositivos de bloco com informações sobre tamanho e pontos de montagem:
```bash
lsblk
lsblk -f  # inclui informações de sistema de arquivos
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINT
```

**fdisk** - Lista partições e tamanhos:
```bash
sudo fdisk -l
sudo fdisk -l /dev/sda  # informações de um disco específico
```

**parted** - Lista partições e tamanhos:
```bash
sudo parted /dev/sda print
```

**iotop** - Monitorar em tempo real:
```bash
sudo iotop
```

## Informações mais detalhadas

**smartctl** - Informações SMART do disco (saúde, modelo, serial):
```bash
sudo smartctl -a /dev/sda
sudo smartctl -H /dev/sda  # apenas status de saúde
```

**hdparm** - Informações técnicas do HD/SSD:
```bash
sudo hdparm -I /dev/sda
```

**du** - Uso de espaço em diretórios:
```bash
du -sh /home  # tamanho total de um diretório
du -h --max-depth=1 /  # tamanho de cada diretório no nível raiz
```
