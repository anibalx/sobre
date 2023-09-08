# PROCESSO ANALÌTICO
* empresa:
  * nome
  * local
  * área de atuação
  * como faz as coisas 
    * cultura 
    * métricas 
    * integração
  * problema a ser ressolvido
    * cenário atual
    * proposta de mudança

---

# BASES DO CI/CD
> 4 Métricas (Accelerate - Karen Leland)
  * Frequência de deploy (QTE por dia)
  * QTE tempo para fazer deploy (commit -> produção)
  * Taxa de falhas
  * Tempo médio para recuperar de falha (MTTS)

---

# ÁREAS DE ANÁLISE DO CI/CD
  * Análise sintática (lint)
  * Complexidade Ciclomática
  * Testes Unitários (coverage)
  * Testes de integração
  * Testes end-to-end (e2e)

---

# PIPELINE IDEAL
  1 source
    * requisições x reviewers
  2 build
    1 compilação do código e das dependências
    2 Roda códigos unitários
    3 cobertura de códigos
  3 ambiente de testes
    * testes de integração
  4 ambiente de produção
    1 alarmes dos errors
    2 latência
    3 métricas chave do negócio
    4 Período de cozimento
      * detecção de anomalias
      * Contagem de errors + latência das breaches
    6 Canary

---

# VALOR GERADO PELO CI
  * Redução de riscos
    * Garante que tudo é integrável
    * que passa nos testes
    * que funciona
  * Reduz processos manuais chatos
    * builds
    * dploys
    * rodas testes
  * Garante que todo código podese entregue
  * Gera uma confiança maior entre o time e o produto

---

# LOCAL DO ARQUIVO QUE CONTÉM OS CI
```sh
  touch meu_projeto/.gitlab-ci.yml
```

---

# ANATOMIA DOS CI

## On
> Rode todas as vezes que houver um pull request para a branch main.
```yml
  name: Integração Contínua
  on:
    pull_request:
      branches:
        - main
    push:

  jobs:
```

> Rode a branch main, logo após o workflow "Integração Contínua"
```yml
  name: Integração Contínua

  on:
    workflow_run:
      workflows: ["Integração Contínua"]
      branches: [main]
      type:
        - completed
```

---

## Jobs
> Estabeleça um job
```yml
  jobs:
    executa_a_parada:
```

---

## Runs-on
> Estabeleça aonde irá rodar
```yml
  jobs:
    executa_a_parada:
      runs_on: ubuntu-latest
```

## Steps
> Estabeleça os passos a serem executados
```yml
  jobs:
    executa_a_parada:
      runs_on: ubuntu-latest
      steps:
```

## Ações -> Uses/Run
> Comandos que, combinados com steps, criam jobs
```yml
      steps:
        - name: Realiza o checkout
          uses: actions/checkout@v2

        - name: Instala o Python 3.9
          uses: actions/setup-python@v2
          with:
            python-version: 3.9
```

### Ações -> Uses/Run | produzidas pela comunidade
> Comandos que, combinados com steps, criam jobs
```yml
      steps:
        - name: Instala Poetry
          uses: Gr1N/setup-poetry@v4
```

### Ações -> Uses/Run | roda os jobs dentro do sistema
> Comandos que, combinados com steps, criam jobs
```yml
      steps:
        - name: Instala as dependências
          run: poetry install

        - name: Executa o Black
          run: poetry run black --check app

        - name: Executa o Isort
          run: poetry run isort --check app
```

---

# EX 
## Exemplo com instalação de ferramentas
* OBS 1: script    == o que deverá rodar linha a linha
* OBS 2: artifacts == o que será baixado após o build
* OBS 3: only      == rode apenas enquanto estiver na master

###  **.gitlab-ci.yml** (ferramentas)
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

## Exemplos de testes com Selenium
### Estrutura de testes deste exemplo
meu_projeto
└── integration              
    └── features       
      └── steps       
        └── environment.py       
        └── tests.feature       
└── unittests                
    └── test_app.py       

### **.gitlab-ci.yml (tests)
* OBS 1: script    == o que deverá rodar linha a linha

```yml
unit-tests:
  image: python
  stage: test
  script:
    - pip install poetry
    - poetry install
    - poetry run python -m unittest discover ./tests/unittest -v 

integration-tests:firefox:
  image: python
  stage: test
  services:
    - selenium/standalone-firefox
  script:
    - pip install poetry
    - poetry install
    - SELENIUM="http:selenium__standalone-firefox:4444/wd/hub" MOZ_HEADLESS=1 poetry run behave tests/integration/features/

integration-tests:chrome:
  image: python
  stage: test
  services:
    - selenium/standalone-chrome
  script:
    - pip install poetry
    - poetry install
    - SELENIUM="http:selenium__standalone-chrome:4444/wd/hub" poetry run behave tests/integration/features/
```

---

# REFERÊNCIAS
[Documentação do GitLab Runner](https://docs.gitlab.com/runner/)
[Como usar GitLab Runner](https://stackoverflow.com/questions/32933174/use-gitlab-ci-to-run-tests-locally)
[Gitlab CI - Live de Python #106](https://www.youtube.com/watch?v=yqsGbfvbMcQ)
[Do Zero ao Deploy #0 - Eduardo Mendes](https://www.youtube.com/watch?v=LpWPijZYWnQ)
[Do Zero ao Deploy #1 - Eduardo Mendes](https://www.youtube.com/watch?v=wDjZGkfphbk)
[Do Zero ao Deploy #2 - Eduardo Mendes](https://www.youtube.com/watch?v=L69ZBHIqPZo)
