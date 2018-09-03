<!-- {"layout": "title"} -->
# PHP - Parte 2
## Inclusão de arquivs PHP, autenticação, arquivos e classes, PDO :crown: x3

---
# O que veremos hoje

1. [Inclusão de arquivos PHP](#inclusao-php)
1. [Sessões e Autenticação](#servidor-apache)
1. [Classes](#classes)
1. [Banco de Dados usando PDO](#pdo)

<!--   1. Instalando Apache, MySQL e PHP
   1. A Atividade-->

<!--*[PHP]: PHP Hypertext Preprocessor*-->
---
<!-- {"layout": "section-header", "slideHash": "servidor-web"} -->
# Inclusão de Arqivos PHP

- Reaproveitamento de HTML/PHP
- include
- include_once
- require
- require_once


<!-- {ul:.content} -->


---
<!-- {"layout": "2-column-content", "slideHash": "for-formas-preferiveis"} -->
## Reaproveitando o HTML/PHP entre paginas
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Piratovelha</title>
    <link rel="stylesheet" href="estilos.css">
  </head>
  <body>
    <p>Ovelha marinha-saqueadora frequentemente vista nas ilhas caribenhas (seu habitat) navegando embarcações de madeira.</p>
		<footer>ovelha@racasraras.com</footer>
  </body>
</html>
```
```html
<!DOCTYPE html>
<html>
  <head>
     <meta charset="utf-8">
     <title>Algod-ovelha</title>
     <link rel="stylesheet" href="estilos.css">
  </head>
  <body>
     <p>Em vez de lã, esta ovelha é uma exímia produtora de algodão e muito apreciada pela indústria têxtil chinesa.</p>
		 <footer>ovelha@racasraras.com</footer>
  </body>
</html>
```
---
## Comando **include**
```php
<?php
	$nomeOvelha = "Algod-ovelha";
 	include("cabecalho.php");
?>
 <p>Em vez de lã, esta ovelha é uma exímia produtora de algodão e muito apreciada pela indústria têxtil chinesa.</p>
<?php
	include("rodape.php");
?>
```
---
<!-- {"layout": "2-column-content"} -->
## Comando **include**
```php
<?php
	$nomeOvelha = "Pira-tovelha";
 	include("cabecalho.php");
?>
 <p>Ovelha marinha-saqueadora frequentemente vista nas ilhas caribenhas (seu habitat) navegando embarcações de madeira.</p>
<?php
	include("rodape.php");
?>
```
```html
<!DOCTYPE html>
<!-- Arquivo: cabecalho.php -->
<html>
 <head>
   <meta charset="utf-8">
   <title><?=$nomeOvelha ?></title>
   <link rel="stylesheet" href="estilos.css">
 </head>
 <body>
```
```html
<!-- Arquivo: rodape.php -->
    <footer>ovelha@racasraras.com</footer>
  </body>
</html>
```
---
## Comandos: include, require

- **include** e **include_once**: caso não encontre o arquivo, será exibido um **warning**. include_once o arquivo é inserido apenas uma vez no script.
- **require** e **require_once**: mesmo funcionamento, porém, neste caso, caso não encontre o arquivo, será exibido um **erro**
---
<!-- {"layout": "section-header", "slideHash": "servidor-web"} -->
# Sessões e Autenticação

- Armazenando informação do usuário em sessões
- Autenticação
- password_hash e password_verify
<!-- {ul:.content} -->
---
## Sessões

- Variáveis guardam valores apenas durante a execução do script PHP
- Se quisermos armazenar dados enquanto o usuário está visitando o site? Por exemplo:
	- Carrinho de compras
	- Páginas visitadas
	- Dados de login
- Em PHP, as sessões são armazenadas em um array associativo `$_SESSION`
- Caso o usuário fique inativo por um periodo (padrão 24 minutos), a sessão é destruida

---
## Sessões - exemplo

- **session_start()**: inicia ou continua uma sessão. Deve ser usada no início de cada script. Caso o script inclua outro, este outro não precisa deste comando.
- **session_id()**: Obtem o id da sessão
- **session_destroy()**: elimina todos os dados da sessão atual.

---
<!-- {"layout": "2-column-content"} -->
```php
<?php
//arquivo: teste1.php
session_start();
$_SESSION["cor_favorita"] = "azul";
?>
```
```php
...
<body>
<p>
 <?php
 //arquivo: teste2.php
 session_start();
 //checa se foi setado a cor favorita
 if(isset($_SESSION["cor_favorita"])){
   print("Cor favorita: ".$_SESSION["cor_favorita"]);
}else{
   print("Ainda não foi setado a cor favorita :()");
}
?>
</p>
	</body>
</html>
```
---
## Passos para autenticação:
- O usuário fornece o login e senha
- Verifica-se se o login e a senha são válidos
- Caso seja válido, setar uma variável na sessão informando que se está autenticado
```php
	$_SESSION["autenticado"] = true;
```
- Em cada página, podemos verificar se o usuário está autenticado:
```php
if(!isset($_SESSION["logado"]) || $_SESSION["logado"] !== true){
	//inclua o php de login (ou redirecione)
}else{
	//inclua o php da página em questao
}
```
- Para redirecionar, use: `header("location: endereco.php");`
---
## Senhas - Criptografia
- Uma senha precisa ser armazenada de forma criptografada.
- password_hash($senha,$algoritmo): criptografa a senha
- password_verify: verifica se a senha em questão é a senha criptografada
```php
//para criptografar
$senha_cript = password_hash("rasmuslerdorf", PASSWORD_DEFAULT);
//armazena $senha_cript no banco de dados
//para checar se a senha que o usuário forneceu está correta
//considere $senhaUsr a senha do usuario e obtenha $senha_cript no BD:
	if (password_verify($senhaUsr, $senha_cript)) {
	    echo 'Senha é válida!';
	} else {
	    echo 'Senha inválida!';
	}

```
---
<!-- {"layout": "section-header"} -->
# Mais sintaxe PHP

- Classes
- yield
- PDO
<!-- {ul:.content} -->
---
# Sintaxe Básica
```php
<?php
class Pessoa{
	private $nome;
	public function __construct($nome){
		$this->nome = $nome;
	}
	public function getNome(){
		return $this->nome;
	}
	public function setNome($nome){
		$this->nome = $nome;
	}

	public static function exMetodoEstatico(){
		return 1;
	}
}
$p = new Pessoa("joao");//instanciação
print($p->getNome());//chamada de método
print(Pessoa::exMetodoEstatico())//chamada de método estatico
```
---
# Comando yield
- Quando usado em um método/função ele é similar a um return, porém, não sai da função após retornar o elemento. Exemplo:
```php
function x(){
	yield "oi";
	yield "tudo";
	yield "joia";
	//seria o mesmo que
	return array("oi","tudo","joia");
}
foreach(x() as el){
	print(el);
}
```
- Ao usar yield, os dados não são armazenados no vetor, assim, há uma economia de memória.
---
# PDO - PHP Data Objects
- Forma mais segura para obter dados no banco de dados.
- Criação da conexão:
```php
$opt  = array(
			PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
			PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
			PDO::ATTR_EMULATE_PREPARES   => FALSE,
	);
	$dsn = 'mysql:host=localhost;dbname=base;charset=utf8';
	$conn = new PDO($dsn, DB_USER, DB_PASS, $opt);
```
---
```php
$query = "SELECT
		nome,
		sobrenome
	FROM
		pessoa
	where
		cidade_id = :cidade";
$stmt = $db->prepare( $query );
$stmt->bindParam(":cidade", $cidadeId);
$stmt->execute();
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)){
	extract($row);
	$pessoa = new Pessoa($nome,$sobrenome);
	print("Pessoa: ".$pessoa->getNome());
}
```



---
# Referências

1. [Site do Apache](http://apache.org)
1. [Guia PHP](http://php.net/manual/pt_BR/langref.php)
2. [Guia MySQL](https://dev.mysql.com/doc/refman/5.7/)
