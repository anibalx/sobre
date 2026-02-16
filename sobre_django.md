# Sumário
1. [Base do Django](#base-do-django)  
2. [manage.py](#manage.py)  
3. [Comandos Mais Utilizados](#comandos-mais-utilizados)
4. [Apps](#apps)
    - [App Padrão](#app-padrão)
    - [Dica Sobre urls.py](#dica-sobre-urls.py)
    - [startproject](#startproject)
    - [startapp](#startapp)  
5. [Inicio de app](#inicio-de-app)
6. [Ative server (project)](#ative-server-project)
    - [Adição de aplicativos (pages)](#adição-de-aplicativos-pages)  
7. [Instalação do app](#-nstalação-do-app)
   - [pages/views.py (exibida no html)](#pages/views.py-exibida-no-html)  
8. [Criação de modelo html dentro do diretótio templates](#criação-de-modelo-html-dentro-do-diretótio-templates)  
    - [Adição de informação dentro do home.html](#adição-de-informação-dentro-do-home.html)  
    - [Adição de rota que liga função de exibição home() a view home.html](#adição-de-rota que-liga-função-de-exibição-home-a-view-home.html)  
9. [Criação do urls em pages, dentro da aplicação](#criação-do-urls-em-pages--dentro-da-aplicação)  
    - [pages/urls.py](#pages/urls.py)   
10. [Adição de estilo no projeto (na raiz do projeto)](#adição-de-estilo-no-projeto-na-raiz-do-projeto)  
    - [Dentro templates/base.html](#dentro-templates/base.html)  
    - [Adição de tags (herança) na aplicação pages](#adição-de-tags-herança-na-aplicação-pages)   
11. [Informando a existência de templates para o projeto](#informando-a-existência-de-templates-para-o-projeto)  
12. [Criação de Modelos (models) Para um App Dentro de Projeto do Django](#criação-de-modelos-models-para-um-app-dentro-de-projeto-do-django)  
13. [Criação de Migrations (models -> database)](#criação-de-migrations-models-->-database)  
    - [Acesso ao shell do Django para construir migrations](#acesso-ao-shell-do-django-para-construir-migrations)
14. [Consulta ao ORM do Django](#consulta-ao-ORM-do-django)  
    - [Função que Terá a Chave Primária do Projeto](#função-que-terá-a-chave-primária-do-projeto)
    - [Consulta de Dentro do Shell do Django](#consulta-de-dentro-do-shell-do-django)
15. [Comentários](#comentários)
    - [Route](#route)
    - [Migrações](#migrações)
    - [HTML pages](#html-pages)
    - [Settings](#settings)

---

# Base do Django
O Django começa numa url, da url vai para a view, a view utiliza o model, o model volta com um dado e a view dá uma response.  

---

# manage.py
Arquivo que permite fazer muita coisa com o Django.  

---

# Comandos Mais Utilizados
```
test
startapp
shell
makemigrations
migrate
check
```

---

# Apps
> Veja cada app como um serviço dentro do Django.  

## App Padrão
```
core
```

## Dica Sobre urls.py
Cria um **urls.ry** dentro de cada app e extende isso para app principal.  

## startproject
A app principal é criada com **startproject**..

### startapp
Já as apps secundárias, são criadas dentro do projeto com startapp, que é como se fosse um service.  

---

# Inicio de app
```
  django-admin <PROJECT_NAME> <DIR_PROJECT> <DIR_IN_DIR_PROJECT>
```  
* No exemplo esboçado acima, dir_in_dir_project === personal_portfolio/personal_portfolio.  

```
  django-admin startproject <DIR_PROJECT> .
```  

```
  django-admin startproject personal_portfolio .
```  

---

# Ative server (project)
```
  python manage.py runserver
```  

## Adição de aplicativos (pages)
```
  python manage.py startapp pages
```  

> Gera o que está abaixo.  
```
  __init__.py = diga ao python que isto é um módulo
  admin.py    = páginas de administração do Django
  apps.py     = configurações do app
  models.py   = classes que ORM do Djnaog converte em tabelas
  tests.py    = classes de teste
  views.py    = funções e classes que manipulam dados a serem exibidos pelo html
```

---

# Instalação do app
> Arquivo de configuração settings.py.  
```
  rp-portfolio/personal_portfolio/settings.py
```  

```
INSTALLED_APPS = [                                                                                                                                                       
  'django.contrib.admin',                                                                                                                                              
  'django.contrib.auth',                                                                                                                                               
  'django.contrib.contenttypes',  
  'django.contrib.sessions',                                                                                                                                           
  'django.contrib.messages',                                                                                                                                           
  'django.contrib.staticfiles',                                                                                                                                        
]
```  

> Diz ao Django que meu app foi criado recentemente.  
```
INSTALLED_APPS = [                                                                                                                                                       
  "pages.apps.PagesConfig",
  'django.contrib.admin',                                                                                                                                            
  'django.contrib.auth',                                                                                                                                             
  'django.contrib.contenttypes',                                                                                                                                     
  'django.contrib.sessions',                                                                                                                                         
  'django.contrib.messages',                                                                                                                                         
  'django.contrib.staticfiles',                                                                                                                                      
]                 
```  

---

# pages/views.py (exibida no html)
> Renderiza uma página html chamada home.html (página ainda não criada).  
```
from django.shortcuts import render

def home(request):
    return render(request, "pages/home.html", {})
```  

---

# Criação de modelo html dentro do diretótio templates
```
mkdir -p pages/templates/pages
```  

```
touch pages/templates/pages/home.html
```  

## Adição de informação dentro do home.html
```
<!-- pages/templates/pages/home.html -->

<h1>Hello, World!</h1>
```  

## Adição de rota que liga função de exibição home() a view home.html
> personal_portfolio/urls.py.  
```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("admin/", admin.site.urls),
    path("", include("pages.urls")),
]
```  

---

# Criação do urls em pages, dentro da aplicação
```
touch pages/urls.py
```  

## pages/urls.py
```
from django.urls import path
from pages import views

urlpatterns = [
    path("", views.home, name='home'),
]
```

---

# Adição de estilo no projeto (na raiz do projeto)
> Cada aplicativo contém seu próprio templates/.  
> Para modelos que todo o projeto compartilha, é uma boa ideia criar um templates/ diretório no diretório raiz.  
```
  mkdir templates
  touch templates/base.html
```  

## Dentro templates/base.html
```
<!-- templates/base.html -->

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>{% block title %}My Personal Portfolio{% endblock title %}</title>
    <link
        href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/css/bootstrap.min.css"
        rel="stylesheet"
    >
</head>
<body class="container">
{% block page_content %}{% endblock page_content %}
</body>
</html>
```  

## Adição de tags (herança) na aplicação pages
```
<!-- pages/templates/pages/home.html -->

{% extends "base.html" %}

{% block page_content %}
    <h1>Hello, World!</h1>
{% endblock page_content %}
```  

---

# Informando a existência de templates para o projeto
> Dentro arquivo: **personal_portfolio/settings.py**.  
```
# ...

TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",
        "DIRS": [
            BASE_DIR / "templates/",
        ],
        "APP_DIRS": True,
        "OPTIONS": {
            "context_processors": [
                "django.template.context_processors.debug",
                "django.template.context_processors.request",
                "django.contrib.auth.context_processors.auth",
                "django.contrib.messages.context_processors.messages",
            ]
        },
    }
]

# ...
```  

---

# Criação de Modelos (models) Para um App Dentro de Projeto do Django
> projects/models.py.  
```
from django.db import models

class Project(models.Model):
    title = models.CharField(max_length=100)
    description = models.TextField()
    technology = models.CharField(max_length=20)
```  

---

# Criação de Migrations (models -> database)
```
(venv) $ python manage.py makemigrations projects
```
# Aplicação das migration no arquivo migrations
```
python manage.py migrate projects
```  

## Acesso ao shell do Django para construir migrations
```
python manage.py shell
```  

> Dentro do shell do Django importe seu projetcts (app criado).  
```
from projects.models import Project

### Cria instância do projeto projects.
>>> first_project = Project(
...     title="My First Project",
...     description="A web development project.",
...     technology="Django",
... )
>>> first_project.save(

### Criação de projetos adicionais.
>>> second_project = Project(
...     title="My Second Project",
...     description="Another web development project.",
...     technology="Flask",
... )
>>> second_project.save()
>>> third_project = Project(
...     title="My Third Project",
...     description="A final development project.",
...     technology="Django",
... )
>>> third_project.save()
>>> exit()
```  

---

# Consulta ao ORM do Django
> projects/views.py  
```
from django.shortcuts import render
from projects.models import Project

def project_index(request):
    projects = Project.objects.all()
    context = {
        "projects": projects
    }
    return render(request, "projects/project_index.html", context)
```  

## Função que Terá a Chave Primária do Projeto
> projects/views.py  
```
# ...
def project_detail(request, pk):
    project = Project.objects.get(pk=pk)
    context = {
        "project": project
    }
    return render(request, "projects/project_detail.html", context)
# ...
```  

## Consulta de dentro do shell do Django
```
# ...
from projects.models import Project

Project.objects.all()

project = Project.objects.get(pk=1)

project.title

project.description
# ...
```  

---

# Comentários

## Route
**route**, é uma sequência que contém um padrão de URL.  

## Migrações
models.py ➜ cria migrações (class for table in database).  
makemigrations ➜ faça as migrações.  
migrate ➜ aplique as migrações.  

## HTML pages
Para chegar numa página html é preciso passar por três partes:  

```
url ------------------------------------------ view ----------------------------------------------------- html
facebook.com/agua               o que fazer quando chegar naquele link                      o que exibir quando chegar na página




rota ------------------------------------- view responsável ------------------------------------------ nome de referência
path('/minha_pagina',                      view.func_name                                              name='home'
```  

## Settings
Sempre é preciso cadastrar o app criado em settings.py.  
