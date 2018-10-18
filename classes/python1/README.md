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
<!-- {"layout": "section-header", "slideHash": "caracteristicas"} -->
# Características da linguagem
## Visão geral da linguagem

- Características
- Aplicações
- Organização dos arquivos

---
## Python

- Linguagem imperativa, com tipagem dinâmica
- Multiplataforma
- Sintaxe sucinta e favorece a legibilidade
- Possibilita **também** orientação a objetos

---
## Aonde é Utilizado

- Desenvolvimento Web ([Django](https://www.djangoproject.com/), [Pyramid](https://pylonsproject.org/))
- Computação Científica e métodos numéricos
- Ensino
- Aplicações Desktop
- Gerenciamento de software
- Scripts em geral

 [Veja exemplos](https://www.python.org/about/apps/)

---
## Principais elementos da linugagem

- Cada **pasta** é chamado de **pacote**

- Cada **arquivo** é considerado um **módulo**

- Dentro de um **módulo** podem existir diversas **classes** ou **funções**

- Todo **pacote** possui o arquivo `__init__.py` que será carregado quando o pacote for chamado


---
<!-- {"layout": "section-header", "slideHash": "sintaxe"} -->
# Sintaxe
## Sintaxe básica da linguagem

- Operadores
- Variáveis
- Tipos de dados
- Listas



---
## Operadores

- Semelhantes aos de C, Java e C#:
  - Aritméticos
    - **`+`** soma
    - **`-`** subtração
    - **`*`** multiplicação
    - **`/`** divisão
    - **`%`** resto da divisão
  - Atribuição
    - **`=`** simples
    - **`+=  /=  %=`** composta
  - Relacionais
    - **`==`** igualdade
    - **`!=`** desigualdade
    - **&lt;  &lt;=** menor/menor igual
    - **&gt;  &gt;=** maior/maior igual
  - Lógicos
    - **`not`** não
    - **`and`** e
    - **`or`** ou
<!-- {ul^4:.multi-column-list-2} -->

- **Não há** operador aritmético de incremento de decremento (**`++`** ou **`--`**)
- Os operadores lógicos são sensíveis a maúisculas e minúsculas

---
## Váriaveis

- Não são declaradas
  - A partir do momento que usamos, começa a existir
- Tipagem dinâmica

  ```python
  nota = 10  # x é inteiro
  nota = "Dó" #x passa ser string
  ```


---
## **Nomes válidos** para variáveis

- <pre style="float: right; margin-left:30px; font-size: 0.75em; color:#111; background: #ddd; border-radius: 10px; padding: 0px 10px 10px 10px">
    <strong>Palavras reservadas:</strong>
      or and not if elif
      return break def exec assert del
      finally import try break
      for in pass while class else from
      is print yield continue except
      global lambda  
  </pre>
  Nomes de variáveis devem:
  - **Começar com:** `_`  ou letras
  - **O restante:** `_` letras e números

---
## Tipos de dados (cont.)
- Númericos: **int**, **float**, **complex**
- Booleano: Assume `True` ou `False` (**_case sensitive_**)
- Strings: Pode ser usado aspas simples ou duplas
- Valores especiais
  - `None`: Vazio
  - `float('inf')`: Infinito
---
## Conversão de valores
- Para convertermos um valor de um tipo de dados usamos as funções:

  - **`str`:** Converter para **string**
  - **`float`:** Converter para **float**
  - **`int`:** Converter para **inteiro**
- A função type exibe o tipo de uma variável
```python
x = 1
y = str(x) #y = '1'
z = float(x) #z = 1.0
w = type(z) == int #w = False
```
---
<!-- {"layout": "regular"} -->
## Concatenação de valores em uma string
  - Se necessário, convertemos as variáveis para string (usando a função `str`)
  - Efetuamos a concatenação
```python
compX = complex('1+2j')
intY = 2
fltZ = 2.5
bolW = True
strDado = "Olá!"
soma = compX+intY+fltZ
strTexto = strDado+" Resultado: "+str(soma)+" Boleano:"+str(bolW)
print(strTexto)
```
:::result
  Olá! Resultado: (5.5+2j) True
:::


<!---
# Estrutura de dados básica
## Estrutura de dados da linguagem
- Vetores

- Conjuntos (na próxima aula)
- Tuplas (na próxima aula)
- Dicionários (na próxima aula)
-->
---
## Listas

- Listas são estruturas de dados unidimensionais, **heterogêneas**
- Os itens das listas **não** precisam ter o mesmo tipo
  ```python
  listaDeCoisas = ['Aew', 35, True, [], 'outra string']
  ```
- Use a função `len` para retornar o tamanho
- Faça indexação usando `[` e `]`
- Usar o método append para adicionar elementos na lista
  ```python
    x = len(listaDeCoisas)  # x = 5
    print(listaDeCoisas[0]) #imprime "Aew"
    listaDeCoisas.append("Nova coisinha") #adiciona 'nova coisinha' no final da lista
  ```
<!---
# Conjuntos

- Similar aos vetores, porém não permite valores iguais
- Transformamos um vetor em conjunto usando a função `set`
- Conjunto não permite valores iguais
--->

---
<!-- {"layout": "section-header", "slideHash": "statements"} -->
# _Statements_
## Funções, Codicionais e estruturas de repetição
- Condicionais: `if`, `else`, `elif`
- repetição: `for`, `while`
---
# _Statements_

- Em uma **função**, **condição** ou **estrutura de repetição**:  
  - seus blocos são definidos por **identação**
  - identação deve ser consistente (pelo número de `tab` ou `espaços`)

- Em condicionais e estrutura de repetição, não é necessário usar parênteses



---
<!-- {"layout": "2-column-content-zigzag"} -->
# Condicionais
```python
if hora < 12:
  manha = True
```
```python
if hora < 12:
  manha = True
else:
  manha = False
```
```python
if (nota>=60) and (nota<70):
  conceito = 'C'
elif (nota>=70) and (nota<80):
  conceito = 'B'
elif nota>=90:
  conceito = 'A'
else:
  conceito = 'F'
```
---
## Estrutura de Repetição Simples  (1/3)


- De `i=0`; enquanto `i<4`<!-- {li:style="display: inline-block; width:30%;border-right:1px dashed black; padding-right: 10px;font-size:0.8em;"}-->
  ```python
  for i in range(4):
    print(i)
  ```
  :::result
  0<br>
  1<br>
  2<br>
  3
  :::
- De i=1; enquanto i<6; passo 2:<!-- {li:style="display: inline-block; width:30%;border-right:1px dashed black; padding-right: 10px;font-size:0.8em;"}-->
  ```python
  for i in range(1,6,2):
    print(i)
  ```
  :::result
  1<br>
  3<br>
  5
  :::
- De i=1; enquanto i<6; passo 2:<!-- {li:style="display: inline-block; width:30%; padding-right: 10px;font-size:0.8em;"}-->
    ```python
    for i in range(1,6,2):
      print(i)
    ```
    :::result
    1<br>
    3<br>
    5
    :::  
```python
>>> range(1,6,2)
[1, 3, 5]
```

---
  Estrutura de Repetição - Percorrendo Listas (2/3)

  - Sem índice:<br><!-- {li:style="display: inline-block; width:43%;border-right:1px dashed black; padding-right: 10px;"}-->
    ```python
    frutas = ['kiwi','pêra']
    for fruta in frutas:
      print(fruta)
    ```
    :::result
    kiwi<br>
    pêra
    :::
  - Com índice:<br><!-- {li:style="display: inline-block; width:52%;"}-->
    ```python
    frutas = ['kiwi','pêra']
    for i,fruta in enumerate(frutas):
      print(str(i)+":"+fruta)
    ```
    :::result
    0: kiwi<br>
    1: pêra
    :::
---
Estrutura de Repetição (2/2)


-
  ```python
  i = 0
  while i<10:
    print(i)
  ```
  :::result
  0 <br>
  1 <br>
  2 <br>
  :::
  <!-- {li:style="display: flex; flex-direction: row; justify-content: space-around;margin-left: 30px;"} -->

---
## Funções

- São declaradas usando a palavra `def`:
  ```python
  def add(a, b):
    return a + b

  x = add(2,5)   # x = 7
  ```


---
# Keywords arguments
- As seguintes chamadas à função possui o mesmo resultado:
```python
x = add(a=2,b=5)
x = add(2,b=5)
```
- `a=2` e `b=2` sãos `keyword arguments` e, os demais, `Positional Arguments`.
- Não é possível colocar `keyword arguments` e, logo após, `Positional Arguments`:
  ```python
  x = add(a=2,5)
  ```
- Resultado: "SyntaxError: positional argument follows keyword argument"
---
## Funções - Valores _default_ (1/2)

- Definindo-se valores _default_ para argumentos. Assim, estes argumentos podem ser omitidos na hora de invocar a função:
  ```python
  def add(a, b=1, c=0):
    return a + b + c

  x = add(2,5,1)   # x = 8
  x = add(2,5)     # x = 7
  x = add(2)     # x = 3
  x = add(2,c=2)     # x = 5
  ```
---
## Funções - Valores _default_ (2/2)

- **Não** é possível colocar um argumento **com** valor _default_ **antes** de argumentos **sem** valores default.
Exemplo:
  ```python
  def add(a, b=1, c):
    return a + b + c
  ```
:::result
SyntaxError: non-default argument follows default argument
:::
---

### Escopo

- O escopo da variavel:
  - Criada dentro da **função**: é visível em toda a função
  - Variáveis fora da **função** e da **classe** é visível em todo o módulo

```python
x = 1
def f(a, b=1, c=0):
  if a>b:
    y = 2
  else:
    y = a+b+c
  return y #Variaveis visiveis aqui: a, b, c, x, y

h = f(1,2,3)#Variáveis visíveis aqui: x,h
```
---
<!-- {"layout": "section-header", "slideHash": "execucao"} -->
# Questões práticas
## Como executar o Python
- Executar comando no terminal
- Ponto inicial de execução
- Console python

---
## Ponto inicial de execução

- Devemos definir o ponto iniciação de execução (ou seja 'o main') usando uma condicional.

```python
def add(a,b):
  return a+b

if __name__ == "__main__":
  x = add(3,1)
  print("Resultado: "+str(x))
```
- A variável `name` armazena qual módulo chamou o determinado arquivo. Quando ele foi chamado pela prompt de comando, `__name__ == "__main__"`

---
## Invocando o main
- Vamos supor que esse arquivo tenha o nome `arquivo.py`. Chamaremos pelo **prompt de comando** como:
  ```
  python arquivo.py
  ```
- Caso se este arquivo estiver dentro de um **pacote** chamado `matematica`. Temos que chamar (de fora do pacote) da seguinte forma:  
```
python  -m matematica.arquivo
```
- Caso você possua mais de uma versão de python na sua maquina, o nome do comando poderá mudar (ex. python3).

- Garanta que o arquivo possua **permissão de execução**

---
## Console python

- É possível `brincar` no console python para testar funcionalidades e executar scripts também. Exemplo:
```shell
hasanzim@maquina:~$ python
Python 3.5.2 (default, Nov 23 2017, 16:37:01)
Type "help", "copyright", "credits" or "license" for more information.
>>> a = 2
>>> b = 3
>>> x = a+b
>>> print(x)
5
```


---
<!-- {"layout": "section-header", "slideHash": "exercicio"} -->
# Execícios
## Exercícios para se sentir confortável com a linguagem

- Pré-exercício
- Criação de funções

---
## Pré-exercicio

- Você deverá criar um arquivo ex. `codigo.py`. Esse arquivo possúirá todas as funções a serem implementadas nos exercícios.

- Você deverá 'criar o main' com exemplo de execução de cada exercício criado

- Para cada função, deve-se aparecer, comentado, o que ela faz e o nome do autor.  Exemplo:
```python
def add(a,b):
  """
  Realiza a soma de dois numeros
  @author: Alice Fernandes
  """
  return a+b

if __name__ == "__main__":
  x = add(2,3)
  print("Soma: "+str(x))
```

---
## Exercícios - Funções

Você deverá fazer as seguintes funções. Não é permitido usar funções prontas da linguagem (ex. somatório usando `sum`). Teste-as 'no main' usando valores fixos:

- `maior(a,b)`: Retorna o maior valor entre a e b
- `soma(lista,x)`: retorna o somatório dos valores passados pela lista. O  argumento `x` deve ser opcional que, se passado, será somado ao resultado final.
- `media(lista)`: Retorna a média dos valores passados pela lista.
- `valores_iguais(lista1,lista2)`: retorna uma lista contendo os valores iguais entre as duas listas passadas como parâmetro
- `indice_prim_valor_igual(lista1,lista2)`: retorna **a posição** na `lista1` do primeiro valor igual ao da `lista2`. Caso não exista, é retornado `None`.

---
# Referências

1. [Guia Python](https://www.python.org/)
1. [Exemplos de aplicações](https://www.python.org/about/apps/)
<!--1. [Simple is Better Than Complex](https://simpleisbetterthancomplex.com/) (em inglês)
1. [Introduction · Django Girls Tutorial](https://tutorial.djangogirls.org/pt/)
1. [Introduction · Django Girls Tutorial](https://tutorial.djangogirls.org/en/) (em inglês)-->
