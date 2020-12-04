

# Dicas de como utilizar o Lumen - sobrinho do Laravel.

 ##  Instalação
```
composer create-project --prefer-dist laravel/lumen=5.8.0 'nome aplicação'
```
## Configuração 
```
// Na Raiz do projeto. Abra o arquivo ".env" e dentro dele vamos primeiramente configurar os dados de acesso ao banco de dados.

DB_HOST=127.0.0.1 // ip do host
DB_PORT=3306 // porta da conexão
DB_DATABASE=base // nome da base de dados
DB_USERNAME=homestead // nome de usuario da base de dados
DB_PASSWORD=secret // senha de acesso a base de dados
```

# Rodando a aplicação
```
// Abra no terminal a pasta da aplicação e execute o código informado para rodar a aplição.

php -S localhost:8000 -t public
```

# Criando Rotas Lumen
> Na pasta **/routes** vai ter o arquivo web.php e dentro dele vai conter todas as rotas do projeto. Esse arquivo e onde configuramos todas as nossas rotas da aplicação.
```php
//Exemplos de rotas simples
$router->get('/teste', function () use ($router) {
	return  'Olá mundo';
});
```
## Rotas com controller
> No exemplo acima mostra a como criar um rota, mas de forma simplificada. Agora vamos ver uma rota com controller. O controller e local onde fica toda a lógica de regra de negócio. Sempre e recomendável criar rotas onde ela indique um constroller.  

```php
// Toda rota indica um controller e todo controller que o seu metodo a ser executado e para isso a lógica e a seguinte "nomeController@NomeDoMetodo"

$router->get('/testeController', 'Teste@index');
``` 

## Criando prefixos (palavra passada para um grupo de rotas)

```
// dessa forma podemos agora acessar a rota '/controller' com o prefixo 'api/controller' e tudo que estiver dentro do grupo vai ter o prefixo para acessar.

$router->group(['prefix' => '/api'], function() use ($router) {
	$router->get('/controller', 'Teste@index');
});
```



# Controller

Controller e o local onde fica toda a lógica de negócios da aplicação. Todas as rotas geralmente direcionam para um controller

## Exemplo De Controller

```php
<?php
// regras para criação de controller - todos controller deve ter o mesmo nome da classe que está dentro dele. Exemplo se o arquivo do controller chama 'Teste.php' a classe deve chamar 'class Teste'

namespace  App\Http\Controllers;
use App\Episodio; // model do controller 
use Illuminate\Http\Request;

class  Teste
{
	public  function  index()
	{
		return  'Olá mundo!!!!!!!!!!!!';
	}
}
```

##  Forma de declarar o controller na rotas
```php
$router->get('/testeController', 'Teste@index'); // informa o controller e o metodo utilizado
```

# Migration 
As migrations são basicamente uma forma de criar banco de dados sem precisar escrever o SQL.  Podemos criar todo o banco de dados direto com PHP e para isso precisamos criar a migrations para depois de criado o escopo e só executar o comando e elas vão ser geradas no banco de dados. ***Nessa etapa de geração de banco de dados com as migrations, o arquivo .env já tem que ter as configurações de acesso ao banco de dados***

## Comando para gerar um migration

Todas as migrations quando criadas vão está no diretório ***/database/migrations/"arquivo da migration"***
```
"php artisan make:migration criar_tabela_instituicao  --create=instituicao"  
```
> Onde -> "criar_tabela_instituicao" e o nome do arquivo da migration.

> Onde -> "instituicao" e o nome da tabela que vai ser criada no banco de dados.

## Estrutura de criação de uma tabela - migration

[Documentação Oficial com os tipos de dados](https://laravel.com/docs/5.8/migrations#creating-columns)

## Exemplo de uma tabela
```php
<?php
use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class  CriarTabelaLogin  extends  Migration
{
	/**
	* Run the migrations.
	*
	* @return  void
	*/

	public  function  up()
	{
		Schema::create('instituicao', function (Blueprint  $table) 	
		{			      
		$table->bigIncrements('id');
		$table->string('nome');
		$table->timestamps();
		});
	}
	/**

	* Reverse the migrations.

	*

	* @return  void

	*/

	public  function  down()
	{
		Schema::dropIfExists('instituicao');
	}
}
```
## Agora que temos a estrutura da tabelas criadas vamos realmente gerar o banco de dados com o comando 

```
php artisan migrate
```

Se a estrutura do banco de dados estiver tudo certo a migration vai ser executada sem nenhum problema.

# Model
Quando falamos em ***model*** e parte que vai trabalhar diretamente com o banco de dados. Toda ***migration/tabela*** tem um arquivo de model. 

Todo model deve está na pasta: ***app/"arquivo do model"***

## Exemplo de model
```php
<?php
namespace  App;
use Illuminate\Database\Eloquent\Model;
class  instituicaoModel  extends  Model
{
	protected  $table = 'instituicao'; // nome da tabela que vai utilizar
	public  $timestamps = true; // informa que o campo de time que e gerado automaticamente vai ficar ativo
	protected  $fillable = ['nome']; // informa qual campo pode 		ser gravado dados
}
```


# Por padrão  e preciso ativar algumas configurações para trabalhar com as querys no banco e para isso precisamos ativar o 'eloquent'

* Para ativar ele e preciso ir na pasta ***' bootstrap/app.php'*** dentro desse arquivo vai conter o seguinte trecho.

```php
// $app->withFacades();
$app->withEloquent(); // e preciso descomentar essa parte para funcionar.
```
