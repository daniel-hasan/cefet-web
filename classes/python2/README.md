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
# Estrutura de Dados
## Outras estruturas de dados

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

nome, num = exemplo() #nome = 'casa' e num = 2948
```
---
## Conjuntos

- Conjunto: coleção **não ordenada** de **elementos únicos**
- Instanciação:
```python
  frutas = {"pera","uva","banana","banana"}
  print(frutas) #imprimirá: {"pera","uva","banana"}
```
---
## Operações com conjuntos

- Interseção: `&`
- União: `|`
- Diferença: `-`
- Pertence: `in`


```python
  cesta1 = {"pera","uva","banana"}
  cesta2 = {"pera","abacaxi"}
  x = cesta1 & cesta2 #x = {"pera"}
  x = cesta1 | cesta2 #x = {"pera","uva","banana","abacaxi"}
  x = cesta1 - cesta2 #x = {"banana","uva"}
  print("abacaxi" in cesta1) #Imprime: False
  print("abacaxi" in cesta2) #Imprime: True
```
---
## Função `set`

- Converte uma elemento iterável em conjunto
- Elemento iterável é qualquer tipo de variável que podemos iterar (usando for, por exemplo):
  - Exemplo: `string`, `vetores`
- Para criarmos um conjunto vazio, executamos `set()` (e não `{}`)

```python
  x = set([1,5,6,9]) #x = {1,5,6,9}
  x = set("casa")    #x = {'c', 'a', 's', 'a'}
  x = set() #x = conjunto vazio
```
---
<!-- {"layout": "section-header", "slideHash": "classes"} -->
# Classes
## Uso de Programação Orientada a Objetos

- Arquivos
- Classes
---
<!-- {"layout": "section-header", "slideHash": "pacotes"} -->
# Pacotes
## Importação e instalação de pacotes

- import
- pip
<!--- requirements
- Ambientes virturais-->
---

<!--```shell
virtualenv --python='/usr/local/bin/python3' envs/env-exploracao-espacial
```
```shell
source envs/crawling-github/bin/activatesource envs/crawling-github/bin/activate
pip freeze
```-->
---
# Testes Unitários
## Testes automatizados

- Tipos de testes
- Integração contínua

---
# Referências

1. [Guia Python](https://www.python.org/)
1. [Exemplos de aplicações](https://www.python.org/about/apps/)
<!--1. [Simple is Better Than Complex](https://simpleisbetterthancomplex.com/) (em inglês)
1. [Introduction · Django Girls Tutorial](https://tutorial.djangogirls.org/pt/)
1. [Introduction · Django Girls Tutorial](https://tutorial.djangogirls.org/en/) (em inglês)-->
