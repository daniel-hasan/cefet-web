<!-- {"layout": "title"} -->
# Django Templates
## Templates, arquivos estáticos e URLs
---
## Principais Componentes  Django

- **Template**: Exibição do html (usualmente, dinâmico)
- **View**: Obtenção da resposta e renderização do **template**. Se necessário, consultando o banco de dados pelos **models**
- **Models**: Responsável pela persistência/gerenciamento dos dados


---
## Arquivos do projeto

![](../../images/dir-django-app.png)

---
## Templates

- Facilita a geração de páginas dinâmicas

- Possui:
  - Parte estática do conteúdo
  - Sintaxe para tratar a parte dinâmica

- **Sintaxe para apresentação**: Não é possível executar códigos Python no template.
---
## Templates - Exemplo na linha de comando

```python
>>> from django.template import engines
>>> django_engine = engines['django']
>>> template = django_engine.from_string("Ola {{ name }}!")
>>> template.render({'name':'Hasan'})
'Ola Hasan!'
```

---
## Templates - Configuração

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'dir_templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            # ... some options here ...
        },
    },
]
```
- [Veja opções do atributo **options** aqui](https://docs.djangoproject.com/en/2.1/topics/templates/#django.template.backends.django.DjangoTemplates)

---
<!-- {"layout": "2-column-content"} -->
## Template inclusão e herança de templates
```html
<html>
  <head>
    <title>Pagina Supimpa - Home</title>
    <link rel="stylesheet" href="estilos.css">
  </head>
  <body>
    <nav><ul><li>Home</li><li>História</li></ul>
    <main>conteudo do home :D</main>
  <body>
</html>
```
```html
<html>
  <head>
    <title>Pagina Supimpa - História</title>
    <link rel="stylesheet" href="estilos.css">
  </head>
  <body>
    <nav><ul><li>Home</li><li>História</li></ul>
    <main>conteudo da história :D</main>
  <body>
</html>
```
---
## Template inclusão e herança de templates
- **principal.html**:<!-- {li:style="display: inline-block; width:60%;border-right:1px dashed black; padding-right: 10px;font-size:0.8em;"}-->
  ```html
  <html>
    <head>
      <title>Pagina Supimpa - {% block titulo %}{% endblock%}</title>
      <link rel="stylesheet" href="estilos.css">
    </head>
    <body>
      {% include "menu.html" %}
      <main>{% block conteudo %}{% endblock%}</main>
    <body>
  </html>
  ```
  **menu.html:**
  ```html
  <nav><ul><li>Home</li><li>História</li></ul>
  ```
- **home.html**:<!-- {li:style="display: inline-block; width:35%;border-right:1px dashed black; padding-right: 10px;font-size:0.8em;"}-->
  ```html
  {% extends "principal.html" %}
  {% block titulo %}Home{% endblock%}
  {% block conteudo %}
  Conteúdo do Home :D
  {% endblock%}
  ```
  **história.html**:
  ```html
  {% extends "principal.html" %}
  {% block titulo %}Hitória{% endblock%}
  {% block conteudo %}
  História :D
  {% endblock%}
  ```
---
## Views

- Views são responsáveis por:
  - Obter e processar a requisição
  - Responder a requisição. Se necessário:
    - Insere/consulta/atualiza/remove instancias
    - Indica o template a ser renderizado
---
## Generic View - Renderização de um template

```python
from django.views.generic.base import TemplateView
class Home(TemplateView):
    template_name = "home.html"
```

---
<!-- { "slideHash": "urls"} -->
## URLs

- O arquivo `urls.py` indica quais URLs estão disponíveis em um projeto Django
- Altere a lista `urlpatterns` deste arquivo com os endereços desejados

```python
from app_projeto.views import *
urlpatterns = [
    path('articles/<int:year>/', Post.as_view(),name='articles_per_year'),
    path('', Home.as_view(),name='home'),
]
```

- Cada elemento da lista possui um `path` com os parametros: endereço, view e nome
- o nome pode ser referenciado no template para ser gerado a url:
  ```html
  <a href='{% url "home" %}'>Home</a>
  <a href='{% url "articles_per_year" year=2003 %}'>2003 Posts</a>
  ```

---
<!-- { "slideHash": "static"} -->
## Arquivos estáticos
- Salvamos os arquivos estaticos (imagens, CSS e JS) em uma pasta separada
- Pasta de nome `static`, por padrão, fica dentro a pasta do **app** podendo ser alterada em `settings.py`
- `load static`: Comando para usarmos os endereços estáticos
- `static`: comando/tag Para que seja renderizado um endereço estático
```html
{% load static %}
<html>
  <head>
    <title>Pagina Supimpa - {% block titulo %}{% endblock%}</title>
    <link rel="stylesheet" href="{% static "estilos.css" %}">
  </head>
  <body>
    {% include "menu.html" %}
    <main>{% block conteudo %}{% endblock%}</main>
  <body>
</html>
```

---
# Referências

1. https://docs.djangoproject.com
1. https://simpleisbetterthancomplex.com/
1. https://tutorial.djangogirls.org/pt/
