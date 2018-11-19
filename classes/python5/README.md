<!-- {"layout": "title"} -->
# Django Templates e Views
## Template (mais sintaxe) e Views

---
## Sintaxe do template

- Impressão de variáveis no HTML
```html
  <p>Ola! Meu nome é <strong>{{nome}}</strong>!
```

- Usar `.` para acesso a chaves de *dicionário*, indices de listas e atributos de objetos
```html
  {{ my_dict.key }}
  {{ my_object.attribute }}
  {{ my_list.0 }}
```
---
## Sintaxe do template

- Condicionais
```html
{% if athlete_list %}
  Atletas: {{ athlete_list|length }}
{% else %}
  Não há atletas.
{% endif %}
```

- Usar `.` para acesso a chaves de *dicionário*, indices de listas e atributos de objetos
```html
<ul>
{% for athlete in athlete_list %}
    <li>{{ athlete.name }}</li>
{% empty %}
    <li>Não há atletas cadastrados </li>
{% endfor %}
</ul>
```
[Mais tags e filtros Django](https://docs.djangoproject.com/pt-br/2.1/ref/templates/builtins)

---
## Views

- Views são responsáveis por:
  - Obter e processar a requisição
  - Responder a requisição. Se necessário:
    - Insere/consulta/atualiza/remove instancias
    - Indica o template a ser renderizado


---
<!-- {"layout": "2-column-content"} -->
## View - Processamento de uma requisição

```python
from django.shortcuts import render
from django.views import View

class Home(View):
  def get(self, request):
    return render(request,
              "home.html",
              {'sobre': [{"titulo":"De onde eles vêm",
                          "texto":"Lorem ipsum dolor sit amet, consectetur"},
                          {"titulo":"O que eles querem",
                          "texto":"osakdpokasdokaspok"},
                          ]})
  ```
  ```html
  {% for item_sobre in sobre %}
    <h2>{{ item_sobre.titulo}}</h2>
    <p>
      <button class="botao-expandir-retrair">+</button>
      {{item_sobre.texto}}
    </p>
  {% empty %}
    Não <strong>há</strong> sobre ainda :-(
  {% endfor %}
```
---
<!-- { "slideHash": "urls"} -->
## URLs

Para criar a URL, referencie a view criada:

```python
from app_projeto.views import *
from django.views.generic.base import TemplateView
urlpatterns = [
    path('', Home.as_view(),name='home'),
]
```

---
<!-- { "slideHash": "urls-params"} -->
## URLs - Processando URL com parametros



URL:
~ ```python
  urlpatterns = [
      path('diga-ola-para:<str:nome>/<str:cidade>', Ola.as_view(), name='oi'),
      ]
  ```
View:
~  ```python
  class Ola(View):
      def get(self, request, nome,cidade):
          return render(request,
                          "ola.html",
                          {'nome_pessoa': nome,'cidade':cidade})
  ```
Template:
~  ```html
    <p>Ola <strong>{{ nome_pessoa }}</strong> de {{cidade}}!</p>
  ```
Ao acessarmos: `http://127.0.0.1:8000/diga-ola-para:Hasan/BH` será renderizado:

```html
  <p>Ola <strong>Hasan</strong> de BH!</p>
```
---
## Uso de form
- Para usarmos formulários HTMLs, primeiramente podemos criar um formulario como uma classe Python. Por exemplo:
```python
from django import forms
class PessoaForm(forms.Form):
    nome = forms.CharField(label='Nome:', max_length=100)
    data_nascimento = forms.DateField(label="Data Nascimento")
```
- Além de renderizar o HTML, formulários fazem a validação, limpeza/tratamento dos dados

---
## Form - Construtor, atributos e Métodos úteis
- Form(dados,arquivos,initial)
  - dados: dicionário com todos os seus campos e valores
  - arquivos: dicionário que para cada campo que é um arquivo, o ponteiro para o mesmo
  - initial: Dados iniciais (se os dados não forem fornecidos)
- **métodos**
  - `is_valid()`: verifica se o formulário está valido
  - `as_ul()`: renderiza em HTML o form como uma lista
  - `as_p()`: renderiza em HTML o form como usando parágrafos
  - `as_table()`: renderiza em HTML o form como uma table (padrão)
- **atributos**
  - `errors`: dicionário com os erros nos campos preenchidos
  - `cleaned_data`: dicionário com os dados já processados
---
## Form - Exemplo no console
```shell
>>> hasan = PessoaForm({"nome":"","data_nascimento":"oioi"})
>>> hasan.errors
{'nome': ['This field is required.'], 'data_nascimento': ['Enter a valid date.']}
>>> hasan = PessoaForm({"nome":"Daniel Hasan","data_nascimento":"1984-04-14"})
>>> hasan.errors
{}
>>> hasan.is_valid()
True
>>> hasan.cleaned_data
{'nome': 'Daniel Hasan', 'data_nascimento': datetime.date(1984, 4, 14)}
>>> hasan.as_p()
'<p><label for="id_nome">Nome:</label>
    <input type="text" name="nome" value="Daniel Hasan" required id="id_nome" maxlength="100">
  </p>
<p><label for="id_data_nascimento">Data Nascimento:</label>
  <input type="text" name="data_nascimento" value="1984-04-14" required id="id_data_nascimento">
</p>'
```
---
## View - Processamento de uma requisição
<style>
pre{
  max-height: 40vh;
}
</style>
- View:<!-- {li:style="display: inline-block; width:60%;border-right:1px dashed black; padding-right: 10px;font-size:0.8em;"}-->
  ```python
    from django.shortcuts import render
    from django.views import View7
    from datetime import date
    from django import forms
    from django.urls.base import reverse
  class PessoaForm(forms.Form):
      nome = forms.CharField(label='Nome:', max_length=100)
      data_nascimento = forms.DateField(label="Data Nascimento")
    class Contato(View):
      def get(self, request):
        return render(request,
                            "contato.html",
                            {"contato":PessoaForm(initial={"data_nascimento":date.today()})})
      def post(self,request):
        form = PessoaForm(request.POST)
        if form.is_valid():
          # processa o formulario (usando form.cleaned_data)
          return HttpResponseRedirect(reverse('success') )

        return render(request, "contato.html", {'contato': form})
  ```
- Template:<!-- {li:style="display: inline-block; width:35%;padding-right: 10px;font-size:0.8em;"}-->
  ```html
    <h2>Contatos</h2>
    <form method="post">
       {% csrf_token %}
       {{ contato }}
       <button>Enviar</button>
    </form>
  ```

[Formas de exibir o formulário](https://docs.djangoproject.com/en/2.1/ref/forms/api/)


---
<!-- { "slideHash": "model-form"} -->
## Model Form

Considere a classe pessoa:
```python
class Pessoa(models.Model):
  nome = models.CharField(max_length=100)
  data_nascimento = models.DateField()

```

Se desejarmos atualizar dados da pessoa por meio de formulários, usamos o ModelForm:
```python
from django import forms
class PessoaForm(forms.ModelForm):
    class Meta:
        model = Pessoa
        fields = ['nome', 'data_nascimento']
        labels = {"data_nascimento": "Data de Nascimento"}
```
---
## ModelForm - Uso

- Construtor: ModelForm(dados,arquivos,instance)
  - `dados`: Valores que foram preenchidos no formulário
  - `arquivos`: Apontador para os arquivos enviados (opcional)
  - `instance`: Instancia a ser alterada (opcional)

Método save: atualiza/insere a entidade de acordo com os dados passados no construtor

---

## Model Form - exemplo no console (1/2)
```shell
>>> class PessoaForm(forms.ModelForm):
...     class Meta:
...         model = Pessoa
...         fields = ['nome', 'data_nascimento']
...         labels = {"data_nascimento": "Data de Nascimento"}

>>> form = PessoaForm()
>>> form.as_p()
'<p><label for="id_nome">Nome:</label>
    <input type="text" name="nome" required id="id_nome" maxlength="100">
 </p>
 <p><label for="id_data_nascimento">Data de Nascimento:</label>
    <input type="text" name="data_nascimento" required id="id_data_nascimento">
 </p>'
```
---
## Model Form - exemplo no console (2/2)
```shell
>>> from datetime import date
>>> form = PessoaForm({"nome":"Dani","data_nascimento":"1990-04-14"},instance=Pessoa.objects.all()[0])
>>> form.as_p()
'<p><label for="id_nome">Nome:</label>
    <input type="text" name="nome" value="Dani" required id="id_nome" maxlength="100">
 </p>
 <p><label for="id_data_nascimento">Data de Nascimento:</label>
    <input type="text" name="data_nascimento" value="1990-04-14" required id="id_data_nascimento">
  </p>'
>>> form.is_valid()
True
>>> form.save()
<Pessoa: Pessoa object (1)>

```

---
<!-- { "slideHash": "model-form-ex"} -->

## View - Fomulários e modelos:



```python

class SalvarPessoa(View):
    def get(self,request): #Requisitou a exibição do formulário
        return render(request,"salvar_pessoas.html",{"pessoa":PessoaForm()})

    def post(self,request):#via post, salva a pessoa
        form = PessoaForm(request.POST,request.FILES)

        if form.is_valid():
            form.save()
            return HttpResponseRedirect(reverse('lista_pessoas') )
        else:
            return render(request,"salvar_pessoas.html",{"pessoa":form})
```


```html
<h2>Inserir Pessoa</h2>
<form method="post">
   {% csrf_token %}
   {{ pessoa }}
   <button>Enviar</button>
</form>
```
---
## Atualizar elemento

```python
class SalvarTesouro(View):
    def get(self,request,id=None): #Requisitou a exibição do formulário
        pessoa = Pessoa.objects.get(id=id) if id != None else None
        return render(request,"salvar_pessoa.html",{"pessoa":PessoaForm(instance=pessoa)})

    def post(self,request,id=None):#via post, salva a pessoa
        pessoa = Pessoa.objects.get(id=id) if id != None else None
        form = PessoaForm(request.POST,request.FILES, instance=pessoa)

        if form.is_valid():
            form.save()
            #se estiver ok, salva e lista as pessoas
            return HttpResponseRedirect(reverse('lista_pessoas') )
        else:
            #caso nao esteja valido, volte a exibir o formulario
            return render(request,"salvar_pessoas.html",{"pessoa":form})
```
---
## Prática

- Objetivo: treinar criação de visões e templates, acesso ao modelo pela visão

[Clique aqui e faça o download](https://github.com/daniel-hasan/cefet-web-pirates-django/archive/master.zip). Instruções no SIGA.

---
# Referências

1. https://docs.djangoproject.com
1. https://simpleisbetterthancomplex.com/
1. https://tutorial.djangogirls.org/pt/
