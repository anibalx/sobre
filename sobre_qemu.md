# QCOW
qcow 
é um formato de arquivo 
para arquivos de imagem de disco 
usado pelo QEMU, 
um monitor de máquina virtual hospedado. 
Ele significa 
"QEMU Copy On Write" e
usa uma estratégia de otimização de armazenamento em disco 
que atrasa a alocação de armazenamento até que seja realmente necessário.

## EX: 
  * CRIA IMAGEM (DISCO VIRTUAL)
    ```sh
        qemu-img create -f qcow2 <DISCO VIRTUAL>.qcow2 10G
    ```  

    * -f == First image format
    ```sh
        qemu-img create -f qcow2 debian.qcow2 10G
    ```  

  * EMULA SISTEMA
    ```sh
      qemu-system-x86_64 -enable-kvm -m <NUMERO> -smp <NUMERO> -name <NAME> -boot d -hda <DISCO VIRTUAL>.qcow2 -cdrom <IMAGEM ISO>
    ```  

    * -enable-kvm == Habilite o suporte de virtualização total de KVM. Esta opção está disponível apenas se o suporte KVM estiver habilitado durante a compilação.
    * -m <NUMERO> == MEMÓRIA | exemplo: 4G
    * -smp <NUMERO> == Especifique o número de núcleos que o convidado tem permissão para usar. O número pode ser maior do que os núcleos disponíveis no sistema host. | exemplo: 4
    * -name <NAME> == nome da máquina
    * -boot <LETRA> == especifica a ordem de boot dos drivers | exemplo: d ou order=d -> primeiro, CD-ROM
    * -hda <DISCO VIRTUAL>.extensão == Defina um disco rígido virtual e use o arquivo de imagem especificado para ele.
    * -cdrom <IMAGEM ISO> == Defina uma unidade de CDROM virtual e use o arquivo de imagem especificado para ela.
    ```sh
      qemu-system-x86_64 -enable-kvm -m 1G -smp 1 -name 'DEBIAN' -boot d -hda debian.qcow2 -cdrom manjaro.iso
    ```  

  * EMULA SEM DECLARAR A ORDEM DE BOOT E SEM IMAGEM (DISCO VIRTUAL)
    > sem declarar **-boot d** e **-hda debian.qcow2**
    ```sh
      qemu-system-x86_64 -enable-kvm -m 1G -smp 1 -name 'DEBIAN' -cdrom debian.iso
    ```  

  * EMULA SEM DECLARAR A ORDEM DE BOOT, SEM IMAGEM (DISCO VIRTUAL) E SEM ESPECIFICAR O FORMATO
    > sem declarar **-boot d**, **-hda debian.qcow2** e **-cdrom debian.iso**
    ```sh
      qemu-system-x86_64 -enable-kvm -m 1G -smp 1 -name 'DEBIAN' debian.iso
    ```  

  * EMULA SISTEMA SEM IMAGEM (DISCO VIRTUAL)
    > sem declarar **-hda debian.qcow2**
    ```sh
      qemu-system-x86_64 -enable-kvm -m 1G -smp 1 -name 'DEBIAN' -boot d -cdrom debian.iso
    ```  

  * EMULA SISTEMA A PARTIR DA IMAGEM (DISCO VIRTUAL)
    > com declaração de **debian.qcow2**
    ```sh
      qemu-system-x86_64 -enable-kvm -m 1G -smp 1 -name 'DEBIAN' -boot d debian.qcow2
    ```  

---
      
# Ligação de diretório entre host e vm (host)
```sh
  qemu-system-x86_64 -virtfs local,path=/home/$USER/Documentos,security_model=none,mount_tag=home_share --enable-kvm -m 2G -smp 4 -name 'Machine' -hda disco_virtual.qcow2
```

## Dentro da máquina virtual
```sh
  mkdir /mnt/shared_folder
```

```sh
  mount -t 9p -o trans=virtio,version=9p2000.L,msize=262144 home_share /mnt/shared_folder
```

# REFERÊNCIAS
[Gentoo Wiki - QEMU](https://wiki.gentoo.org/wiki/QEMU/Options)
[Arch Wiki - QEMU](https://wiki.archlinux.org/title/QEMU)
