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

# LOCAL DO ARQUIVO QUE CONTÉM AS ACTIONS
  ```sh
    mkdir -p meu_projeto/.github/workflows/
    touch meu_projeto/.github/workflows/continous_integration.yml
  ```
---

# ANATOMIA DAS ACTIONS

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



## Jobs
> Estabeleça um job
```yml
  jobs:
    executa_a_parada:
```

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

# EX **continous_integration.yml**
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

---

# EX **roda_paralelo.yml**
> Execução dos jobs em paralelo
```yml
  name: Integração Contínua

  on:
    pull_request:
      branches:
        - main
    push:

  jobs:
    executa_black:
      runs_on: ubuntu-latest
      steps:
        - name: Realiza o checkout
          uses: actions/checkout@v2

        - name: Instala o Python 3.9
          uses: actions/setup-python@v2
          with:
            python-version: 3.9

        - name: Instala Poetry
          uses: Gr1N/setup-poetry@v4

        - name: Instala as dependências
          run: poetry install

        - name: Executa o Black
          run: poetry run black --check app

    executa_isort:
      runs_on: ubuntu-latest
      steps:
        - name: Realiza o checkout
          uses: actions/checkout@v2

        - name: Instala o Python 3.9
          uses: actions/setup-python@v2
          with:
            python-version: 3.9

        - name: Instala Poetry
          uses: Gr1N/setup-poetry@v4

        - name: Instala as dependências
          run: poetry install

        - name: Executa o Isort
          run: poetry run isort --check app
```

# EX **deploy_manual.yml** deploy manual em Heroku
> Execução dos jobs em paralelo
```yml
  name: Deploy Manual

  on: workflow_dispatch

  jobs:
    deploy_app:
      runs_on: ubuntu-latest
      steps:
        - name: Realiza o checkout
          uses: actions/checkout@v2

        - name: Deploy no Heroku
          uses: akhileshns/heroku-deploy@v3.12.12
          with:
            heroku_api_key: ${{secrets.HEROKU_API_KEY}}
            heroku_app_name: "app_name"
            heroku_email: "email_user"
```

---

# EX **deploy_automatico.yml** deploy manual em Heroku
> Execução dos jobs em paralelo
```yml
  name: Deploy Automático

  on: workflow_dispatch

  jobs:
    deploy_app:
      runs_on: ubuntu-latest
      steps:
        - name: Realiza o checkout
          uses: actions/checkout@v2

        - name: Deploy no Heroku
          uses: akhileshns/heroku-deploy@v3.12.12
          with:
            heroku_api_key: ${{secrets.HEROKU_API_KEY}}
            heroku_app_name: "app_name"
            heroku_email: "email_user"
```

---

# COMMIT LOCAL 
> Rode os commits localmente
```sh
  act
```

---

# REFERÊNCIAS
[Documentação do GitHub Runner](https://docs.github.com/pt/actions)
[Act](https://github.com/nektos/act)
[Github Actions - Live de Python #170 - Com Willian Lopes](https://www.youtube.com/watch?v=L1f6N6NcgPw)
