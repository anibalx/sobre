# INFORMAÇÕES CHS
  * (C)ilinders -> Cilindros
  * (H)eaders -> CABEÇAS
  * (S)ectors -> Setores
```sh
  fdisk -l
```

# TESTES
## dd
Antes de formatar o pendrive
```sh
  dd if=/dev/zero of=/dev/sdc bs=8M count=1
```

## dcfldd
Instalação do dcfldd
```sh
  apt install dcfldd
```

Utilização do dcfldd
```sh
  dcfldd if=/dev/zero of=/dev/sdc bs=1M
```

Utilização do comando cmp, que compara dois arquivos byte a byte
> Se o comando falhar antes do final da unidade (8GB, 16GB etc.), a unidade não poderá ser mais usada,
```sh
  cmp /dev/zero /dev/sdc
```

# ERROS
check:
	checksun not check -> superblock corrupt

label:
	superblock checksum does not match

UUID:
	superblock checksum does not match

format:
	ok
		dosfstools mtools
		unable to read the contents of this file systems

disk:
  /dev/sdd: unrecognised disk label


## ERROS EM INGLÊS
  Throw it
    According to my experience, this pen-drive is damaged. More exactly, the controller (between the USB and the flash memory) seems to have failed. Or it detected a critical problem and went into read-only-mode. With cheap compact devices, it happens quite often due to heat issues.

    This assumes you have checked for the obvious issues including an unreliable connection (check for bent contacts, try a different computer or USB port).

## ERROS EM PORTUGUÊS
  Jogá-lo
    De acordo com minha experiência, este pen-drive está danificado. Mais exatamente, o controlador (entre o USB e a memória flash) parece ter falhado. Ou detectou um problema crítico e entrou no modo somente leitura. Com dispositivos compactos baratos, isso acontece com bastante frequência devido a problemas de calor.

    Isso pressupõe que você verificou os problemas óbvios, incluindo uma conexão não confiável (verifique se há contatos dobrados, tente um computador ou porta USB diferente).



# REFERÊNCIAS
[](https://unix.stackexchange.com/questions/651770/usb-disk-showsunrecognised-disk-label-unable-to-do-dd-partition-or-reformat)
[](https://www.linuxquestions.org/questions/linux-newbie-8/unrecognised-disk-label-gparted-4175586946/)
[](https://ubuntuforums.org/showthread.php?t=2245549)
