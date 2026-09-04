Para criar um disco RAM (ramdisk) no Linux de forma rápida e prática, use o sistema de arquivos virtual tmpfs. Crie uma pasta de destino e monte o espaço usando o comando mount informando o tamanho desejado em megabytes ou gigabytes. [1, 2, 3, 4] 
## Criando o disco RAM manualmente

* Crie uma pasta para usar como ponto de acesso:
```sh
sudo mkdir -p /mnt/ramdisk
```

* Monte o tmpfs definindo o limite de tamanho (exemplo de 2 GB):
```sh
sudo mount -t tmpfs -o size=2G tmpfs /mnt/ramdisk
```

* Verifique se o disco está ativo:
```sh
df -h /mnt/ramdisk [1, 4] 
```

## Tornando a montagem permanente no boot
Para que o disco RAM seja recriado automaticamente toda vez que o sistema ligar, adicione a linha correspondente ao arquivo de configuração de sistemas de arquivos. [5] 

* Abra o arquivo /etc/fstab com um editor de texto (como o nano):
sudo nano /etc/fstab
* Adicione a seguinte linha no final do arquivo:
tmpfs /mnt/ramdisk tmpfs defaults,size=2G 0 0
* Salve e feche o arquivo. [6, 7, 8, 9] 

Se você precisar de ajuda para definir permissões de usuário específicas para essa pasta ou quiser configurar um sistema de cache automatizado, me avise!

[1] [https://askubuntu.com](https://translate.google.com/translate?u=https://askubuntu.com/questions/152868/how-do-i-make-a-ram-disk&hl=pt&sl=en&tl=pt&client=sge)
[2] [https://www.linuxbabe.com](https://translate.google.com/translate?u=https://www.linuxbabe.com/command-line/create-ramdisk-linux&hl=pt&sl=en&tl=pt&client=sge)
[3] [https://webhosting.de](https://webhosting.de/pt/criando-um-ramdisk-sob-linux/)
[4] [https://www.vivaolinux.com.br](https://www.vivaolinux.com.br/dica/Montar-particao-na-memoria-RAM/)
[5] [https://www.youtube.com](https://www.youtube.com/watch?v=65ZnOvY7TNw&t=2)
[6] [https://www.homehost.com.br](https://www.homehost.com.br/blog/tutoriais/linux/como-particionar-o-hd-no-linux/)
[7] [https://docs.redhat.com](https://docs.redhat.com/pt/documentation/red_hat_enterprise_linux/7/epub/installation_guide/guia-de-instalao.epub)
[8] [https://www.digitalocean.com](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-20-04-pt)
[9] [https://www.homehost.com.br](https://www.homehost.com.br/blog/tutoriais/linux/como-particionar-o-hd-no-linux/)

