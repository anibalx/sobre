# TRANSLATE SHELL 
  ## DOCKER
    docker pull soimort/translate-shell
           OU
    wget git.io/trans
    chmod +x trans

  ## CRIAÇÂO DE UM LINK SIMBÓLICO (NÃO OBRIGATÓRIO)
    ln -s "$(pwd)/trans" "${HOME}/.local/bin/translate"

  ## EXECUÇÂO
    * -shell == execute em um shell
    * -brief == exiba a resposta de maneira reduzida
    * -S || -list-engines == lista as engines 
    * -e <ENGINE> == escolhe a engine
    * :pt-br == traduz para portuguès do Brasil
    * en:pt-br == traduz do inglês para portuguès do Brasil
  ```
    docker run -it soimort/translate-shell -shell
    docker run -it soimort/translate-shell -shell -brief
  ```
           OU
  ```
    ./trans
    ./trans -shell -brief
    ./trans -brief :pt-br "Helo, world"
    ./trans -brief :pt-br "Hello, world"
    ./trans -shell -brief :pt-br "Hello, world"
    ./trans -shell -brief en:pt-br
    ./trans -S
    ./trans -e yandex
  ```

  
# LibreTranslate
  ## DOCKER
  * -it == entre atréves do shell
  * --rm == remova o container caso já exista
  * -p == publique o container numa porta (ou intervalo de portas)
  ```
    docker run -it --rm -p 5000:5000 libretranslate/libretranslate
  ```


# Argos Translate (Offline)
  ## Configure o poetry para que a venv permaneça dentro do diretório de desenvolvimento
  ```
    poetry config virtualenvs.in-project true
  ```
  ## Criação de um novo projeto Poetry
  ```
    poetry new <DIRETÓRIO> ; cd <DIRETÓRIO>
  ```
    Veja o exemplo abaixo:
    ```
      poetry new translate_py ; cd translate_py
    ```
  ## Adição do Pip
  ```
    poetry add pip
  ```
  ## Instalação do Argos Translate por meio do Pip
  ```
    pip3 install --user argostranslategui
    pip3 install argostranslate argostranslategui
  ```
  ## Construção do alias para adentrar ao venv com mais facilidade
  ```
    source <DIRETÓRIO>/.venv/bin/activate
  ```
    Veja o exemplo abaixo:
    ```
        alias argostranslate='source ${HOME}/translate_py/.venv/bin/activate'
    ```
  ## Execução (dentro do ambiente virtual .venv)
  ```
    argos-translate-gui'
  ```
[](https://blog.pronus.io/posts/python/gerenciamento-de-versoes-ambiente-virtuais-e-dependencias-com-pyenv-e-poetry/)
