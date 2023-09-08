# Sistema (como um todo)
> runlevel em system-V; em Systemd == alvo
```sh
  systemd-analyze                          # tempo de boot
  systemd-analyze time                     # tempo de boot
  systemd-analyze blame                    # tempo de boot (ordem descendente)
  systemd-analyze security                 # segurança dos serviços
  systemd-analyze syscall-filter <ARG>     # filtra as syscall
  systemctl --failed                       # verifica quais serviços falharam
  systemctl status                         # status dos serviços 
```

# Estado
> Verifica como está o estado do serviço (semáforo)
```sh
  systemctl status                         # status dos serviços 
  systemctl stop                           # para dos serviços 
  systemctl start                          # inicia serviços 
  systemctl restart                        # para e reinicia serviços 
  systemctl list-unit-files --type=service # mostra estado dos serviços
```

# Comportamento
> Estado do serviço assim que a máquina entra em funcionamento (assim que termina o boot)
```sh
  systemctl enable <SERVICE> --now        # habilita sem reboot
  systemctl disable <SERVICE> --now       # desabilita sem reboot
  systemctl is-enable <SERVICE>           # verifica se serviço está habilitado
  systemctl mask <SERVICE>                # não deixa iniciar serviço
  systemctl unmask <SERVICE>              # volta a deixar iniciar serviço
  systemctl list-units -t service         # lista todos os serviços
  systemctl --no-pager                    # retira paginação
  systemctl cat <SERVICE>                 # características do serviço
```

# Nível
```sh
  systemctl get-default                   # alvo padrão
  systemctl isolate multi-user.target     # ambiente gráfico para
  systemctl set-default multi-user.target # habilita novo alvo padrão
  systemctl set-default graphical.target  # habilita novo alvo padrão
  systemctl isolate graphical.target      # ambiente gráfico funciona
```

---


## ModeManager.service
  is a DBus-activated daemon that controls mobile broadband (2G/3G/4G) interfaces. If you don’t have a mobile broadband interface — built-in, paired with a mobile phone via Bluetooth, or USB dongle — you don’t need this.
  é um daemon ativado por DBus que controla interfaces de banda larga móvel (2G/3G/4G). Se você não tem uma interface de banda larga móvel — built-in, emparelhado com um telefone móvel via Bluetooth, ou dongle USB — você não precisa disso.

  Only if your system is going to act like a modem for something else and/or you use dial-up in some form. For example … ‘mobile broadband’.
  Só se o seu sistema vai agir como um modem para outra coisa e / ou você usa dial-up em alguma forma. Por exemplo ... ‘banda larga móvel’.

[How can I remove modem-manager from boot?](https://askubuntu.com/questions/216114/how-can-i-remove-modem-manager-from-boot)
[Kill modem-manager process](https://askubuntu.com/questions/45726/kill-modem-manager-process)
[Freedesktop](https://www.freedesktop.org/)
[Como posso remover o modem-manager do boot?](https://sobrelinux.info/questions/7197/how-can-i-remove-modem-manager-from-boot)


## accounts-daemon.service 
  is a potential security risk. It is part of AccountsService, which allows programs to get and manipulate user account information. I can’t think of a good reason to allow this kind of behind-my-back operations, so I mask it.
  é um risco de segurança potencial. Faz parte do AccountsService, que permite que os programas obtenham e manipulam as informações da conta de usuário. Eu não consigo pensar em uma boa razão para permitir este tipo de operações atrás de mim, então eu mascarei.


## avahi-daemon.service 
  is supposed to provide zero-configuration network discovery, and make it super-easy to find printers and other hosts on your network. I always disable it and don’t miss it.
  é suposto fornecer a descoberta de rede de configuração zero, e torná-lo super fácil para encontrar impressoras e outros hosts em sua rede. Eu sempre desabilitei e não perca isso.


## brltty.service 
  provides Braille device support, for example, Braille displays.
  fornece suporte de dispositivo Braille, por exemplo, mostra Braille.


## debug-shell.service 
  opens a giant security hole and should never be enabled except when you are using it. This provides a password-less root shell to help with debugging systemd problems.
  abre um buraco de segurança gigante e nunca deve ser ativado, exceto quando você está usando-o. Isso fornece um shell raiz sem senha para ajudar na depuração de problemas systemd.


## pppd-dns.service 
  is a relic of the dim past. If you use dial-up Internet, keep it. Otherwise, you don’t need it.
  é uma relíquia do passado. Se você usar a Internet dial-up, mantê-lo. Caso contrário, você não precisa.


## rtkit-daemon.service 
  sounds scary, like rootkit, but you need it because it is the real-time kernel scheduler.
  soa assustador, como rootkit, mas você precisa dele porque é o agendador de kernel em tempo real.


## 3whoopsie.service 
  is the Ubuntu error reporting service. It collects crash reports and sends them to https://daisy.ubuntu.com. You may safely disable it, or you can remove it permanently by uninstalling apport.
  é o serviço de relatórios de erros do Ubuntu. Ele coleta relatórios de acidente e os envia para https://daisy.ubuntu.com. Você pode desabilitá-lo com segurança, ou você pode removê-lo permanentemente desinstalando o aporte.


## wpa_supplicant.service 
  is necessary only if you use a Wi-Fi network interface.
  é apenas necessário caso use o uma interface de rede Wi-Fi


## containerd.service
  é um daemon container
  Como não existam contêineres Linux no espaço do kernel, 
  os contêineres são vários recursos do kernel unidos, 
  quando você está construindo uma grande plataforma ou sistema distribuído, 
  você deseja uma camada de abstração entre seu código de gerenciamento e 
  as syscalls e a fita adesiva de recursos para executar um contêiner. 
  É aí que vive o containerd. 
  Ele fornece uma camada de cliente 
  de tipos que as plataformas podem construir sem ter que descer para o nível do kernel. 
  É muito melhor trabalhar com os tipos Container, 
  Task e Snapshot do que gerenciar chamadas para clone() ou mount()
[What is containerd?](https://www.docker.com/blog/what-is-containerd-runtime/)
[Getting started with containerd](https://containerd.io/docs/getting-started/)


---

## Serviços desabiltados
  systemctl disable bluetooth.service --now
  systemctl disable wpa_supplicant.service --now
  systemctl disable udisks2.service --now
  systemctl disable docker.service --now
  systemctl disable docker.socket --now
  systemctl disable cups.service --now
  systemctl disable cups.socket --now
  systemctl disable privoxy.service --now
  systemctl disable containerd.service --now
