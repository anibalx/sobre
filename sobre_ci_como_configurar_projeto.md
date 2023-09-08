# CRIAÇÃO DE DIRETÓRIO BASE
  ```sh
    mkdir -p meu_projeto
  ```


# ENTRADA NO DIRETÓRIO BASE
  ```sh
    cd meu_projeto
  ```


# VERSÃO DA LINGUAGEM 
Selecione a versão da linguagem a ser utilizada.
Neste exemplo, será usada linguagem Python.
Aqui, pode-se usar a ferramenta que desejar.
Contudo **pyenv** (própria ao Python) e **asdf** (Package managemment) são usados.

## pyenv
  > Gera um arquivo .python-version  
  ```sh
    pyenv install <VERSION>
    pyenv local <VERSION>
  ```

## asdf
  * <VERSION> == versão do Python escolhida para usar dentro daquele projeto
  * <local>  == local: permanece apenas dentro daquele projeto (raiz/folhas) 
  * <global> == global: global, vai para todo o sistema.
  ```sh
    asdf plugin-add python
    asdf install python <VERSION>
    asdf <local | global> python <VERSION>
  ```


# GESTÃO DE AMBIENTES (VIRTUAIS)
Selecione a ferramenta para gerência os ambientes virtuais de seu projeto.
Isso permitirá uma mais fácil gerência de suas dependências.
Aqui, o **PIPx** e o **ASDF** serão utilizados para a instalação do **Poetry**.
  ```sh
    pipx install poetry
  ```
  > Note a repetição de comandos a partir do asdf.
  > * __negativo__ == repete comando e só muda os nomes.
  > * __positivo__ == permite unificar e generalizar a instalação das ferramentas. 
  ```sh
    asdf plugin-add poetry
    asdf install poetry <VERSION>
    asdf <local | global> poetry <VERSION>
  ```

## Poetry
  ```sh
    poetry init                 # inicia a estrutura do projeto
    poetry shell                # inicia ambiente virtual
    poetry add <PACKAGE>        # adiciona pacote ao projeto
    poetry add --dev <PACKAGE>  # adiciona pacote para desenvolvimento do projeto
  ```


# FERRAMENTA DE VERSIONAMENTO DE CÓDIGO
O **git** permite a gerência de modificações do código.
Quando auxiliado a um repositório remoto, o código fica resistente.
  ```sh
    git init                        # inicia o controle de versão
  ```

## Gitignore
  Antes de continuar, crie um .gitignore.
  Isso para que o git não versione aquilo que se deseja ignorar.
  Não se esqueça de preenche-lo, vá em gitignore.io.
  ```sh
    touch .gitignore
  ```
  ```sh
    git add -p .                    # seleciona mudanças a se adicionar
    git commit -m "<MENSAGEM>"      # grava as modificações
    git push                        # sobe as modificações para repositório online
  ```


# ESTRUTURA (BASE) DO PROJETO
  ```sh
    meu_projeto
    ├── .gitignore        # o que se deseja ignorar
    ├── .python.version   # arquivo produzido por pipx: guarda a versão do python
    ├── poetry.lock       # arquivo produzido por poetry: guarda as versões das libs
    ├── pyproject.toml    # arquivo produzido por poetry: guarda as informações das libs
    ├── README.md         # arquivo de informações sobre o projeto
    ├── LICENSE           # arquivo que contém a licença sob a qual está este software
    ├── .git              # diretório que guarda as informações sobre as versões do código
    ├── .venv             # diretório que guarda as informações sobre os ambientes virtuais
    └── docs              # diretório que guarda as documentações do projeto
        └── index.md       
    └── meu_projeto       # diretório que guarda os códigos do projeto
    └── tests             # diretório que guarda os testes dos projeto
        └── __init__.py
  ```


# ESCOLHA DO FRAMEWORK DE TESTES
Utilizado para o entendimento do contexto do código.
  * OBS 1: será realizada a instalação de uma ferramenta, mas existem outras.
  * OBS 2: não os padrões de testes utilizados nesta seção de instalação.

## Adiciona framework
  O **Pytest** será adicionado apenas como dependência de desenvolvimento. 
  Pelo fato de ser relativo ao momento de desenvolvimento, apenas.
  Caso fizesse parte do código, --dev seria retirado.
  * OBS 1: o Poetry já cria um diretório tests com um arquivo __init__.py. 
  * OBS 2: __init__.py é necessário para o funcionamento do Pytest.
  * OBS 2: caso o Poetry não tenha criado um diretório tests, crie você.
  ```sh
    poetry add --dev pytest     # instalação do pytest
    pytest                      # roda os testes
  ```

## Estrutura com um teste
  * OBS 1: pytest: busca diretório docs e arquivos iniciados por test.
  ```sh
    └── tests             # diretório que guarda os testes dos projeto
        └── __init__.py
        └── test_meu_test.py
  ```


# ADICIONA UM FORMATADOR DE CÓDIGO
Para que haja uma padronização do modo de codar, utiliza-se uma ferramenta que formata o código de quem desenvolve.
Neste exemplo, será utilizada a ferramenta chamada **blue**.
  ```sh
    poetry add --dev blue       # instalação do blue
    blue .                      # roda o blue para todos os arquivos
  ```
Também será utilizada a ferramenta **isort**, que ordena os imports (em Python)
  ```sh
    poetry add --dev isort      # instalação do isort
    isort .                     # roda o isort para todos os arquivos
  ```


# ADICIONA UM CONSTRUTOR DE DOCUMENTAÇÃO
Documentar um projeto é essencial. 
**Mkdocs** serve para isso, será a ferramenta instalada.
  * OBS 1: o comando mkdocs new . cria o diretório docs, caso já não exista.
  ```sh
    poetry add --dev mkdocs     # instalação do mkdocs
    mkdocs new .                # cria os arquivos index.md e mkdocs.yml dentro do diretório docs
  ```

## Estrutura após comando mkdocks new .
  * OBS 1: index.md    -> armazena a documentação
  * OBS 2: mkdocks.yml -> armazena o nome do site da documentação
  ```sh
    └── docs              # diretório que guarda as documentações do projeto
        └── index.md       
        └── mkdocs.yml       
  ```


# ANÁLISE ESTÁTICA (CHECAGEM, LINTER)
Procuram manter os códigos em conformidade com uma forma simples de desenvolver.
Além disso, busca garantir uma acessível leitura posterior do código.

## BUSCAM
  * Erros de sintaxe
  * Pontenciais problemas
    1 Nomes duplicados
    2 Nomes ruins
    3 Códigos inseguros
  * Análise de complexidade de códigos
  * Violações de códigos

## Ferramenta (em Python)
Será utilizada a ferramenta **prospector**, que comporta várias outras ferramentas para especifícações.
  ```sh
    poetry add --dev prospector   # instalação do prospector
    prospector                    # roda as análises
    prospector --with-tool pep257 # roda as análises relativas à PEP 257
    prospector --doc-warning      # roda as análises relativas a docs
  ```


# VERIFICAÇÃO DE SEGURANÇA
Selecione as ferramentas para verificar a integridade das libs usadas.
  * OBS 1: adicionado ao contexto de desenvolvimento.
  * OBS 2: será realizada a instalação de uma ferramenta, mas existem outras.
  ```sh
    poetry add --dev pip-audit   # instalação do pip-audit
  ```


# FERRAMENTAS UTILIZADAS
 * pyenv | asdf
 * pipx  | asdf
   - git
   - poetry
     * pytest
     * blue
     * isort
     * mkdocs
     * prospector
     * pip-audit


# FERRAMENTAS EXTRAS
* flake8        ➜ checador da pep-8
* pylint        ➜ padronização, conversões e erros
* pydocstyle    ➜ checador da pep-257
* bandit        ➜ problemas de segurança
* radon         ➜ busca de complexidade de código
* prospector    ➜ agregador de ferramentas (Flake8, Mccabe, Pylint, PEP-8, PEP-257)
* mypy          ➜ checador de sugestões de tipo


# AUTOMAÇÕES DE CÓDIGOS
Busca evitar o excesso de programas a instalar um a um.
Aqui, **GNU Make** será utilizado na criação de uma Makefile.
  * OBS: essa é a formulação do make
  ```sh
  # Este é o Makefile.

  #.PHONY == make evita de procurar no sistema
  .PHONY venv install format lint test sec

  # @ == serve para o make não mostrar o programa que está sendo executado.

  venv:
    @poetry shell

  install:
    @poetry install

  format:
    @blue .
    @isort .

  lint:
    @blue --check .
    @isort --check .
    @prospector --with-tool pep257 --doc-warning --no-autodetect

  test:
    @pytest -v

  sec:
    @pip-audit
  ```

  ```sh
    make           # executa todos os comandos
    make venv      # executa o venv
    make install   # executa o install
    make format    # executa o format
    make lint      # executa o lint
    make test      # executa o test
    make sec       # executa o sec
  ```


# CONFIGURAÇÃO DE PRÉ-ADIÇÂO 
> (GIT HOOKS)

O git possui formas de verificação, usadas antes de alguma adição de código.
Dentro do diretório .git/hooks repousam esse scripts: os **hooks**.
Para este exemplo, será criado um arquivo específico: pre-commit.amostra.
  ```sh
    touch meu_projeto/.git/hooks/pre-commit.amostra
    chmox +x meu_projeto.git/hooks/pre-commit.amostra  # permissão de execução
  ```

Nesta parte, este arquivo será preenchido com comandos do Makefile já criado.
  ```sh
    make lint
    make test
  ```

Agora, adicione e commit os arquivos normalmente.
  ```sh
    git add meu_projeto/arquivo_principal.py
    git commit -m "Teste de hooks."
  ```


# CONFIGURAÇÃO DE REPOSITÒRIO EXTERNO 
> (GITHUB ACTIONS, GITLAB PIPELINES, BITBUCKET BAMBOO)

## GitHub Actions 
Existe mais um nível de verificação para seu código, no repositório externo.
Neste exemplo, será utilizado o **GitHub Actions**.

### Crie um repositório e o arquivo de exemplo.
  ```sh
    mkdir -p meu_projeto/.github/workflows/
    touch meu_projeto/.github/workflows/continous_integration.yml
  ```

### Preencha o arquivo **continous_integration.yml**.
  ```yml
    name: Continous Integration
    on: [push]
    jobs:
      lint_and_test:
        runs-on: ubuntu-latest
        steps:

          - name: Set up python
            uses: actions/setup-python@v2
            with:
                python-version: 3.10.2

          - name: Check out repository
            uses: actions/checkout@v2

          - name: Install poetry
            uses: snok/install-poetry@v1
            with:
                virtualenvs-in-project: true

          - name: Load cached venv
            id: cached-poetry-dependencies
            uses: actions/cache@v2
            with:
              path: .venv
              key: venv-${{ hashFiles('**/poetry.lock') }}

          - name: Install dependencies
            if: steps.cached-poetry-dependencies.outputs.cache-hit != 'true'
            run: poetry install --no-interaction

          - name: Lint
            run: poetry run make lint

          - name: Run tests
            run: poetry run make test
  ```

## GitLab CI 
Existe mais um nível de verificação para seu código, no repositório externo.
Neste exemplo, será utilizado o **GitLab CI**.

### Crie um o arquivo de exemplo.
  ```sh
    touch meu_projeto/.gitlab-ci.yml
  ```

### Preencha o arquivo **.gitlab-ci.yml**.
  * OBS 1: script    == o que deverá rodar linha a linha
  * OBS 2: artifacts == o que será baixado após o build
  * OBS 3: only      == rode apenas enquanto estiver na master
  ```yml
    image: python:latest

    stages:
      - nome_do_stage
      - testes
  
    before_script:
      - apt update -y
      - apt upgrade -y

    nome_do_stage:
      stage: nome_do_stage
      script:
        - echo "Apenas um teste do GitLab CI e nada mais."
        # - pip install jedi blue isort radon prospector
        # - blue .

      artifacts:
        paths:
          - meu_projeto

      only:
        - master

    
    testes:unitarios:
      stage: testes
      script:
        - python -m unittest .
  ```
