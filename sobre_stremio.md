# INSTALL PACKAGES
## Site
[GitHub Stremio para Debian](https://github.com/Stremio/stremio-shell/blob/master/DEBIAN.md)
## Debian ***.deb***
```
    apt install libkf5webengineviewer-dev libqt5webview5-dev\
    libmpv-dev qml-module-qtwebchannel qml-module-qt-labs-platform\
    qml-module-qtwebengine qml-module-qtquick-dialogs\
    qml-module-qtquick-controls qtdeclarative5-dev libqt5opengl5-dev\
    librsvg2-bin cmake
```

## Debian ***src***
### Download do repositório  
```
    git clone --recurse-submodules -j8 git://github.com/Stremio/stremio-shell.git
```  
### Instalação de pacotes extras
```
    apt install qtcreator qt5-qmake qt5-default g++ pkgconf libssl-dev libmpv-dev libqt5webview5-dev libkf5webengineviewer-dev qml-module-qtwebchannel qml-module-qt-labs-platform qml-module-qtwebengine qml-module-qtquick-dialogs qml-module-qtquick-controls qtdeclarative5-dev
```  
### Entre na pasta execute os comandos _qmake_ e _make_
```
    cd stremio-shell
    qmake
    make
```
### Baixe o servidor
```
    wget https://dl.strem.io/four/v4.4.111/server.js ; wget https://dl.strem.io/four/v4.4.111/stremio.asar
```
### Execute o Stremio
```
    ./stremio
```

## Pacotes extras caso dê erro na instalação
```
    apt --fix-broken install
    apt install qml-module-qt-labs-platform qml-module-qtquick-controls qml-module-qtquick-dialogs qml-module-qtwebchannel qml-module-qtwebengine libfdk-aac1

```

# CONFIGURE STREMIO DESKTOP
```
    sudo nano /usr/share/applications/stremio.desktop
```

# STREMIO DESKTOP
```
    [Desktop Entry]
    Name=Stremio
    Comment=Stremio
    Type=Application
    Encoding=UTF-8
    Exec=/home/rui/stremio-shell/build/stremio
    Icon=/home/rui/stremio-shell/images/stremio.png
    Categories=GNOME;Application;Development;
    Terminal=false
    StartupNotify=true
```

# STREMIO Debian ***.sh***
```
    #!/usr/bin/env bash

    #
    # Autor: zeiger
    #
    # ---------------------------------------------------- #
    # O QUE ESTA PORRA FAZ?
    #
    #  Executa stremio no Debian.
    #
    #  OBS: siga os procedimentos de instalação do Stremio,
    #	a partir do github do desemvolvedor:
    #
    #  github Stremio:
    #	https://github.com/Stremio/stremio-shell
    #
    #  github Stremio para Debian 10 (stable):
    #	https://github.com/Stremio/stremio-shell/blob/master/DEBIAN.md
    #
    # ---------------------------------------------------- #
    # CHANGELOG:
    #
    #   v0.0.1 09/05/2021, zeiger.
    #
    #
    # ---------------------------------------------------- #
    # TESTADO EM
    #
    #   bash 5.0.11(1)-release; bash 5.0.16(1)-release
    #   zsh 5.8 (x86_64-suse-linux-gnu)
    #
    # ---------------------------------------------------- #
    # REFERÊNCIAS:
    #
    #	site: 		https://meleu.sh/
    #	matéria: 	Como lidar com parâmetros passados na linha de comando em shell scripts
    #	link: 		https://meleu.sh/parametros/
    #
    #	site: 		http://www.dicas-l.com.br/
    #	matéria: 	Argumentos em Shell Scripts
    #	link: 		http://www.dicas-l.com.br/arquivo/argumentos_em_shell_scripts.php#.Xmz9p3VKjZs


    function _help(){
    printf "
    Usage:

        ./stremio.sh [--options]

    Options:

        -h, --help             Help.
        --stremio              Execute Stremio.
        --end		   Finish Stremio.
        --pid		   PID Stremio.

    "
    }

    function _stremio(){

        # Executa o servidor para stremio através do node
        # nohup node ${HOME}/stremio-shell/server.js & >-

        # Execução do stremio
        nohup "${HOME}"/stremio-shell/build/stremio & >-
    }

    function _end_stremio(){
    pkill stremio && pkill node
    }

    function _pid(){
        ps aux | grep --color=auto [s]tremio
    }


    case "$1" in
        --stremio)
            _stremio
        ;;
        --end)
            _end_stremio
        ;;
        --pid)
            _pid
        ;;
        -h | --help | *)
            _help
        ;;
    esac

    exit 0
```
# STREMIO OPENSUSE ***.sh***
```
    #!/usr/bin/env bash

    #
    # Autor: zeiger
    #
    # ---------------------------------------------------- #
    # O QUE ESTA PORRA FAZ?
    #
    #  Executa stremio no OpenSuse.
    #
    #  OBS: siga os procedimentos de instalação do Stremio,
    #	a partir do github do desemvolvedor:
    #
    #  github Stremio:
    #	https://github.com/Stremio/stremio-shell
    #
    #  github Stremio para OpenSuseLeap15:
    #	OBS: instalação também funcional para OpenSuse Tumbleweed
    #
    #	https://github.com/Stremio/stremio-shell/blob/master/OpenSuseLeap.md
    #
    # ---------------------------------------------------- #
    # CHANGELOG:
    #
    #   v0.0.1 14/03/2020, zeiger.
    #
    #
    # ---------------------------------------------------- #
    # TESTADO EM
    #
    #   bash 5.0.11(1)-release; bash 5.0.16(1)-release
    #   zsh 5.8 (x86_64-suse-linux-gnu)
    #
    # ---------------------------------------------------- #
    # REFERÊNCIAS:
    #
    #	site: 		https://meleu.sh/
    #	matéria: 	Como lidar com parâmetros passados na linha de comando em shell scripts
    #	link: 		https://meleu.sh/parametros/
    #
    #	site: 		http://www.dicas-l.com.br/
    #	matéria: 	Argumentos em Shell Scripts
    #	link: 		http://www.dicas-l.com.br/arquivo/argumentos_em_shell_scripts.php#.Xmz9p3VKjZs


    function _help(){
    printf "
    Usage:

        ./stremio.sh [--options]

    Options:

        -h, --help             Help.
        --stremio              Execute Stremio.
        --end		   Finish Stremio.
        --pid		   PID Stremio.

    "
    }

    function _stremio(){

        # Executa o servidor para stremio através do node
        nohup node ${HOME}/stremio-shell/server.js & >-

        # Execução do stremio
        nohup ${HOME}/stremio-shell/stremio & >-
    }

    function _end_stremio(){
    pkill stremio && pkill node
    }

    function _pid(){
        ps aux | grep --color=auto [s]tremio
    }


    case "$1" in
        --stremio)
            _stremio
        ;;
        --end)
            _end_stremio
        ;;
        --pid)
            _pid
        ;;
        -h | --help | *)
            _help
        ;;
    esac

    exit 0
```

# REFERENCES
## Debian
[libqt5opengl5-dev](https://github.com/samaaron/sonic-pi/issues/2032)
[How to Create Custom Desktop Files For Launchers on Linux](https://linuxconfig.org/how-to-create-custom-desktop-files-for-launchers-on-linux)
