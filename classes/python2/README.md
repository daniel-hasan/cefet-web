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
## Listas - operações úteis

```python
lista = ["Alice","Bob","Carol","Bob","Débora"]
lista.sort() #ordena a lista
listaConcat = lista[1:5] #retorna uma lista a partir da posição 1 até a posição 4
listaConcat = lista[:5] #retona uma lista da posição 0 até a posição 4
listaConcat = lista[2:] #retorna a lista sem as psições 0 e 1
lista.insert(0,"Carlos") #adiciona 'Carlos' no inicio da lista

```
- **sort**: os tipos devem ser compatíveis para ordenação
- [Clique aqui para ver documentação completa](https://docs.python.org/3.5/tutorial/datastructures.html#more-on-lists)
---
## Strings  - operações úteis

```python
x = "({ddd}) {telprefixo}-{telfinal}".format(ddd=31,telprefixo=555,telfinal=9875)#x = '(31) 555-9875'
y = "uma frase de impacto"
termos = y.split(" ") #termos = ['uma','frase','de','impacto']
z = "casa".replace("a","x") #z = 'cxsx'
z = "casa".upper() #z = "CASA"
#strings podem ser tratadas como uma lista de caracteres
w = y[0] #w= 'u'
w = y[4:] #w = 'frase de impacto'
frutas = ", ".join(["pera","uva","banana"]) #frutas = "pera, uva, banana"

```
[Veja lista completa de métodos](https://docs.python.org/3.5/library/stdtypes.html#string-methods)

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
- Cada elemento deve ser `hashable`, ou seja:
  - Imutável
  - Implementa os métodos: `__hash__()`, `__eq__()` ou `__cmp__()`
  - Exemplos: string, inteiro, float, tuplas
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
  - As **chaves** são `hashable`
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
  ```
  :::result
  cidade<br>
  nome<br>
  altura

  :::
- Pelo **valor**:<!-- {li:style="display: inline-block; width:27%;border-right:1px dashed black; padding-right: 10px;font-size:0.8em;"}-->
  ```python
  x = {"nome":"hasan",
  print(chave)
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
<!-- {"layout": "section-header", "slideHash": "classes"} -->
# Classes
## Uso de Programação Orientada a Objetos

- Declaração
- Construtor  e Instanciação
- Atributos estáticos e não estáticos
- Anotação `@property`
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
- Colocamos com prefixo `_` atributos/métodos para **informarmos** que são privados
  - Python não possui atributos que sejam verdadeiramente privados
- O prefixo `__` é apenas para indicar que o método/atributo não será sobreposto pelas subclasses
- Se criarmos um atributo `__a`, ainda podemos acessá-lo de maneira pública usando `_Nome-da-classe__a()`

---
## Anotação `@property` e o Encapsulamento
- Vamos supor que temos nossa classe Pessoa
```python
class Pessoa():
  def __init__(self,nome,data_nascimento=date.today()):
    self.nome = nome
```

- Desejamos, agora, alterar o atributo `nome` para `prim_nome` e `ult_nome`.
- Como fazer isso sem alterar os locais em que o atributo `nome` foi chamado? Por exemplo:
```python
joao = Pessoa("João")
joao.nome = "João da Silva"
```
---
## Anotação @property
- Usada para sobrecarregar a atribuição e obtenção de um atributo
- Atributos calculados:<!-- {li:style="display: inline-block; width:45%;border-right:1px dashed black; padding-right: 10px;font-size:0.8em;"}-->
  ```python
  class Funcionario():
    def __init__(self,nome,salario):
      self.nome = nome
      self.salario = salario
    @property
    def salario_liquido(self):
      return self.salario*0.8
  ```

- Encapsulamento:<!-- {li:style="display: inline-block; width:50%;font-size:0.8em;"}-->
  ```python
  class Funcionario():
    def __init__(self,nome,salario):
      self.nome = nome
      self._salario = salario
    @property
    def salario(self):
      return self._salario
    @salario.setter
    def salario(self,val):
      if(val<0):
        raise ValueError("Erro: não é possível salário negativo")
      self._salario = val
  ```
---
## Atributo @property - Acesso ao atributo

```python
  joao = Funcionario('João',234)
  print(joao.salario_liquido)
  joao.salario = 345
  print(joao.salario)
  joao.salario_liquido = 45 #erro 'AttributeError: can't set attribute'
```
---
## Alteração do atributo `nome` da classe Pessoa
```python
class Pessoa():
  def __init__(self,nome,data_nascimento=date.today()):
    self.nome = nome
  @property
  def nome(self):
    return "{prim} {sobrenome}".format(prim=self.prim_nome,sobrenome=self.sobrenome)
  @nome.setter
  def nome(self,val):
    if(len(val)==0):
      return
    arr_nomes = val.split(" ")
    self.prim_nome = arr_nomes[0] if len(arr_nomes)>0 else ""
    self.sobrenome = " ".join(arr_nomes[1:])
```
- Assim, o código abaixo irá funcionar, sem ser modificado:
```python
joao = Pessoa("João")
joao.nome = "João da Silva"
```

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
