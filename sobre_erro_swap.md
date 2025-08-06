# ERRO
```
Gave up waiting for suspend/resume device ao iniciar o Linux (Debian)

Summing some of the advices given here and there
```  

---

## Em EN

1. first make the swap partition work again by
```
sudo mkswap /dev/sda9
```  

> (where sda9 should be the corresponding partition on your system. Check gparted to ensure this. This will DESTROY all your data if you use it on a data partition, like your /home one)  

2. then compute the UUID of the new swap partition
```
sudo blkid /dev/sda9
```  

3. change the UUID code in both these files
```
/etc/fstab
(only change the one concerning /dev/sda9!)
/etc/initramfs-tools/conf.d/resume
```  

4. rebuild the initramfs with
```
update-initramfs -u
```  

5. reboot
> OBS.: You can also change back the swap UUID with this command (thanks Lowell)  
```
mkswap -U UUID /dev/swapdev
```  

> Where UUID is the ID shown in both mentioned /etc files (the ID should be the same in both them, otherwise follow the 1-3 steps!)  

---

## Em PT_BR

Resumindo alguns dos conselhos dados aqui e ali

1. primeiro faça a partição swap funcionar novamente
```
sudo mkswap /dev/sda9
```  

> (onde sda9 deve ser a partição correspondente em seu sistema. Verifique gparted para garantir isso. Isso DESTRUIRÁ todos os seus dados se você usá-lo em uma partição de dados, como a sua / home)  

2. então calcule o UUID da nova partição swap
```
sudo blkid /dev/sda9
```  

3. alterar o código UUID em ambos os arquivos
```
/etc/fstab
```  

> (apenas altere o que diz respeito a /dev/sda9!)  
```
/etc/initramfs-tools/conf.d/resume
```  

4. reconstruir o initramfs com
```
update-initramfs -u
```  

5. reinicie
> Você também pode alterar o UUID de troca com este comando (obrigado Lowell)  
```
mkswap -U UUID / dev / swapdev
```  
> onde UUID é o ID mostrado em ambos os arquivos / etc mencionados (o ID deve ser o mesmo em ambos, caso contrário, siga as etapas 1-3!)  

---

# REFERÊNCIAS
[Gave up waiting for suspendresume device ao iniciar o Linux Debian - Blog Viva o Linux](https://www.vivaolinux.com.br/topico/Iniciantes-no-Linux/Gave-up-waiting-for-suspendresume-device-ao-iniciar-o-Linux-Debian)  
