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

# REFERÊNCIAS
[Gentoo Wiki - QEMU](https://wiki.gentoo.org/wiki/QEMU/Options)
[Arch Wiki - QEMU](https://wiki.archlinux.org/title/QEMU)
