# ESTRUTURA DE PASTAS:
```
        app/
        |   features/
        |   |   steps/
        |   |   |   NOME_DO_MEU_ARQUIVO_DE_TESTE.py
        |   |   NOME_DO_MEU_APP.feature

```  

---

# COMO SE DÃO AS FEATURES:
        
```
    language:en

    Feature: showing off behave

      Scenario: run a simple test
         Given we have behave installed
          When we implement a test
          Then behave will test it for us!


    language:pt

    Funcionalide: exibindo o  behave

      Cenário: rode um teste simple
         Dado que o behave está instalado
          Quando um teste for implementado
          Então behave testará isto para nós!
```  

---

# COMO SE DÁ O ARQUIVO QUE TESTA AS FEATURES:
```py
  from behave import *

  @given('que o behave está instalado')
  def step_impl(context):
      pass

  @when('um teste for implementado')
  def step_impl(context):
      assert True is not False

  @then('behave testará isto para nós!')
  def step_impl(context):
      assert context.failed is False
```  

---

# REFERÊNCIAS
[Behave](https://behave.readthedocs.io/en/latest/)  
[Behave Code in GitHub](https://github.com/behave/behave)  
[Live de Python #10 - Testando comportamento com Python + Behave Parte 1](https://www.youtube.com/watch?v=ReELqf9B86g)  
[Live de Python #10 - Testando comportamento com Python + Behave Parte 2](https://www.youtube.com/watch?v=9EvoggLUp1E)  
[Live de Python #83 - BDD com python e flask](https://www.youtube.com/watch?v=aX0P5tsiat4)  
[Criando uma API com flask + BDD + TDD + Marshmallow](https://www.youtube.com/watch?v=Y_GQdxRSnIg)  
