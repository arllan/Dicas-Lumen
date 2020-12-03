# Dicas de como utilizar o Lumen - sobrinho do Laravel.

 * ***Instalação***
```
composer create-project --prefer-dist laravel/lumen=5.8.0 'nome aplicação'
```
* ***Configuração*** 
```
// Na Raiz do projeto. Abra o arquivo ".env" e dentro dele vamos primeiramente configurar os dados de acesso ao banco de dados.

DB_HOST=127.0.0.1 // ip do host
DB_PORT=3306 // porta da conexão
DB_DATABASE=base // nome da base de dados
DB_USERNAME=homestead // nome de usuario da base de dados
DB_PASSWORD=secret // senha de acesso a base de dados
```

* ***Rodando a aplicação****
```
// Abra no terminal a pasta da aplicação e execute o código informado para rodar a aplição.

php -S localhost:8000 -t public
```
