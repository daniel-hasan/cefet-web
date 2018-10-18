<!-- {"layout": "title"} -->
# Python - Parte 1
## Características e Delícias da linguagem

---
<!-- {"layout": "regular"} -->
# Roteiro

1. [Características da linguagem](#caracteristicas)
1. [Sintaxe Básica](#sintaxe)
1. [Estrutura de dados](#estruturaDados)
1. [_Statements_](#statements)
1. [Questões práticas](#execucao)


---
<!-- {"layout": "section-header", "slideHash": "estruturaDados"} -->
# Mais coleções
## Outras coleções e seus métodos/funções úteis

- Conjuntos
- Tuplas
- Dicionários
- Funções/métodos úteis

---
## Tuplas

- Similar à listas, porém imutável
- Instanciação (duas formas):
```python
  x = (1,4,5)
  x = 1,4,5
```
- Caso haja apenas um elemento, deveremos colocar uma virgula no final ex: `x = 'casa',` ou `x=('casa',)`
- Útil para atribuições e para retornar, em uma função, mais de um valor
```python
def exemplo():
  return "casa",2948

x,y = 1,5# x = 1 e y = 5
nome, num = exemplo() #nome = 'casa' e num = 2948

```
---
## Conjuntos

- Conjunto: coleção **não ordenada** de **elementos únicos**
- Uso:
```python
  frutas = {"pera","uva","banana","banana"} #instanciação
  print(frutas)
  for fruta in frutas: #percorrendo  valores
    print(fruta)
```
---
## Operações com conjuntos

- Interseção: `&`
- União: `|`
- Diferença: `-`
- Pertence: `in`
- adicionar um elemento: `add`


```python
  cesta1 = {"pera","uva","banana"}
  cesta2 = {"pera","abacaxi"}
  x = cesta1 & cesta2 #x = {"pera"}
  x = cesta1 | cesta2 #x = {"pera","uva","banana","abacaxi"}
  x = cesta1 - cesta2 #x = {"banana","uva"}
  cesta1.add("cebola")#cesta1={"pera","uva","banana","cebola"}
  print("abacaxi" in cesta1) #Imprime: False
  print("abacaxi" in cesta2) #Imprime: True
```
---
## Função `set`
- Inicializa um conjunto como conjunto vazio
- Converte uma elemento iterável em conjunto
- Elemento iterável é qualquer tipo de variável que podemos iterar (usando for, por exemplo):
  - Exemplo: string, conjuntos e listas
- Para criarmos um conjunto vazio, executamos `set()` (e **não** `{}`)

```python
  x = set([1,5,6,9]) #x = {1,5,6,9}
  x = set("casa")    #x = {'c', 'a', 's', 'a'}
  x = set() #x = conjunto vazio
```
---
## Dicionários (1/2)
- Mapeia uma **chave** a um **valor**
  - As **chaves** são `hashable`, ou seja:
    - Imutáveis
    - Possui os métodos: `__hash__()`, `__eq__()` ou `__cmp__()`
    - Exemplos: string, inteiro, float, tuplas
  - Os **valores** podem ser qualquer tipo de dado
- Uso:
```python
x = {} #inicia um dicionário vazio
x['Alice'] = 3
x[23] = 5
x[32,32] = 10# x = {(32, 32): 10, 'Alice': 3, 23: 5}
idc_remissivo = {'casa':{1,3},'verde':{3,5,6}}
idc_remissivo['casa'].add(7) #idc_remissivo = {'casa':{1,3,7},'verde':{3,5,6}}
```
---
## Dicionários (1/2)
```python
from datetime import datetime #inclusão do módulo datetime
voo = {
    'companhia': 'Gol',
    'numero': 815,
    'decolagem': {
        'IATA': 'SYD',
        'horario': datetime(2005, 7, 14, 12, 30),#
        'cidade': 'Sydney'
    },
    'chegada': {
        'IATA': 'LAX',
        'horario': datetime(2005, 7, 14, 15, 30),
        'cidade': 'Los Angeles'
    }
}
#imprimirá: 2005-07-14 12:30:00
print(voo['decolagem']['horario'])
```
---
## Dicionários - erros e funções úteis (1/2)
- Erro ao tentar acessar uma chave inexistente:
```python
x = {"Alice":16, "Bob":19, "Carol": 20}
print(x["Débora"])
```
```python
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'Débora'
```
---
## Dicionários - erros e funções úteis (2/2)

- `in`: Verifica se um chave existe:
- `keys()`: Retorna a lista de chaves
- `values()`: Retorna a lista de valores
- `items()`: Retorna a lista de itens (Tupla `(chave,valor)`)
``
```python
x = {"Alice":16, "Bob":19, "Carol": 20, "Débora":21}
if "Débora" in x:
  print("A chave 'Débora' possui o seguinte valor: "+str(x['Débora']))

y = x.keys() #y = ['Débora', 'Alice','Bob','Carol']
y = x.values() #y = [19, 16, 20, 21]
y = x.items() #y = [('Débora',21), ('Alice',16),('Bob',19),('Carol', 20)]
```
---
## Dicionários - Navegando nos elementos
- Pela **chave**:<!-- {li:style="display: inline-block; width:25%;border-right:1px dashed black; padding-right: 10px;font-size:0.8em;"}-->
  ```python
  x = {"nome":"hasan",
      "altura":1.77,
      "cidade":"Belo Horizonte"}
  for chave in x.keys():
      print(chave)
  ```
  :::result
  cidade<br>
  nome<br>
  altura

  :::
- Pelo **valor**:<!-- {li:style="display: inline-block; width:27%;border-right:1px dashed black; padding-right: 10px;font-size:0.8em;"}-->
  ```python
  x = {"nome":"hasan",
      "altura":1.77,
      "cidade":"Belo Horizonte"}
  for valor in x.values():
      print(valor)
  ```
  :::result
  hasan<br>
  1.77<br>
  Belo Horizonte
  :::
- Pela **chave** e **valor**<!-- {li:style="display: inline-block; width:40%;font-size:0.8em;"}-->
  ```python
  x = {"nome":"hasan",
      "altura":1.77,
      "cidade":"Belo Horizonte"}
  for ch,val in x.items():
      print(ch+": "+str(val))
  ```
  :::result
  cidade: Belo Horizonte<br>
  altura: 1.77<br>
  nome: hasan
  :::


- O dicionário não é ordenado
---
## Estruturas heterogêneas - Exemplo
```python
profs_web = [{"nome":"Hasan","cidade":"Belo Horizonte"},
             {"nome":"Coutinho","cidade":"Belo Horizonte"}]
for prof in profs_web:
    print("Professor: "+prof['nome']+" Cidade: "+prof['cidade'])
```
:::result
Professor: Hasan Cidade: Belo Horizonte<br>
Professor: Coutinho Cidade: Belo Horizonte
:::

---
## Listas - operações úteis



---
## Strings  - operações úteis
- format, split, replace, upper, lower, substrings...


---
<!-- {"layout": "section-header", "slideHash": "classes"} -->
# Classes
## Uso de Programação Orientada a Objetos

- Declaração
- Construtor  e Instanciação
- Atributos estáticos e não estáticos
- Anotação `@property`
- Métodos estáticos, não estáticos e abstratos
- Herança simples e múltipla
---
## Declaração
```python
from datetime import date
class Pessoa():
  #construtor possui o nome __init__
  def __init__(self, nome):
    self.nome = nome
    self.telefones = []
  #método simples
  def adiciona_telefone(self,tel):
    self.telefones.append(tel)
  #transforma o objeto numa string ao executar str(objeto)
  def __str__(self):
    return "{nome} - {telefones}".format(nome=self.nome,
                                        nascimento=self.data_nascimento.strftime("%d/%m/%y"))
```
- **`self`**: representa o **objeto corrente**  
- **Atributos**: devem ser criados no contrutor, atribuindo um valor a ele
- **Métodos**: Similar às funções porém, o primeiro argumento **deve** ser o objeto corrente (`self`)
---
## Instanciação
```python
jose = Pessoa("José")
jose.adiciona_telefone("31-5555-5555")
jose.nome = "José Pereira"
print(jose.telefones) #imprime ["31-5555-5555"]
print(jose.nome) #imprime 'José Pereira'
print(jose) #imprime "José Pereira - 17/10/2018 - ['31-5555-5555']"
```
- Os atributos são publicos.
- Colocamos com prefixo "_" atributos **informarmos** que são privados
- Podemos usar a anotação `@property` para alterar o comportamento de um atributo
---
## Atributos estáticos
- São criados dentro da classe
```python
import datetime date
class Pessoa():
  PESSOAS_CRIADAS = 0

  def __init__(self,nome,data_nascimento=date.today()):
    self.nome = nome
    self.data_nascimento = data_nascimento
    self.telefones = []
    Pessoa.PESSOAS_CRIADAS += 1
```

```python
  jose = Pessoa("José")
  maria = Pessoa("Maria")
  print(Pessoa.PESSOAS_CRIADAS) #Imprime 2
```

---
# Referências

1. [Guia Python](https://www.python.org/)
1. [Exemplos de aplicações](https://www.python.org/about/apps/)
<!--1. [Simple is Better Than Complex](https://simpleisbetterthancomplex.com/) (em inglês)
1. [Introduction · Django Girls Tutorial](https://tutorial.djangogirls.org/pt/)
1. [Introduction · Django Girls Tutorial](https://tutorial.djangogirls.org/en/) (em inglês)-->
