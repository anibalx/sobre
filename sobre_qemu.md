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
  * CRIA IMAGEM
    ```sh
        qemu-img create -f qcow2 <DISCO VIRTUAL>.qcow2 10G
    ```
      ### EX: 
        * -f == First image format
    ```sh
        qemu-img create -f qcow2 manjaro.qcow2 10G
    ```

  * EMULA SISTEMA
    ```sh
      qemu-system-x86_64 -enable-kvm -m <NUMERO> -smp <NUMERO> -name <NAME> -boot d -hda <DISCO VIRTUAL>.qcow2 -cdrom <IMAGEM ISO>
    ```
      ### EX:
      * -enable-kvm == Habilite o suporte de virtualização total de KVM. Esta opção está disponível apenas se o suporte KVM estiver habilitado durante a compilação.
      * -m <NUMERO> == MEMÓRIA | exemplo: 4G
      * -smp <NUMERO> == Especifique o número de núcleos que o convidado tem permissão para usar. O número pode ser maior do que os núcleos disponíveis no sistema host. | exemplo: 4
      * -name <NAME> == nome da máquina
      * -hda <DISCO VIRTUAL>.extensão == Defina um disco rígido virtual e use o arquivo de imagem especificado para ele.
      * -cdrom <IMAGEM ISO> == Defina uma unidade de CDROM virtual e use o arquivo de imagem especificado para ela.
   
      ```sh
        qemu-system-x86_64 -enable-kvm -m 1G -smp 1 -name 'MANJARO' -boot d -hda manjaro.qcow2 -cdrom manjaro.iso
      ```

      
# Ligação de diretório entre host e vm
```sh
  qemu-system-x86_64 -virtfs local,path=/home/rui/Documentos,security_model=none,mount_tag=home_share --enable-kvm -m 2G -smp 4 -name 'Machine' -hda disco_virtual.qcow2
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
