# Ambiente de Desenvolvimento com Docker

Este repositório contém uma configuração de Docker para um ambiente de desenvolvimento que suporta PHP 8.3, NGINX, MySQL 8.0 e Node.js 23.0.0. Este projeto é ideal para desenvolvimento com Laravel, PHP puro ou WordPress.

## Estrutura do Projeto

- A pasta `app` é onde você deve colocar seus arquivos PHP.
- A pasta `mysql` é onde os dados do banco de dados são armazenados.
- A pasta `config` contém os arquivos de configuração do NGINX e PHP.
- O arquivo `.env` contém as variáveis de ambiente para o Docker Compose.
- O arquivo `docker-compose.yml` contém a configuração do Docker Compose.
- O arquivo `.gitignore` contém os arquivos que não devem ser versionados.


````
/docker_setup 
├── app 
├── mysql 
├── config 
│ ├── nginx 
│ │ ├── default.conf 
│ │ └── Dockerfile 
│ └── php 
│   ├── local.ini 
│   └── Dockerfile
├── .env 
├── .gitignore 
└── docker-compose.yml
````


## Pré-requisitos

- [Docker](https://www.docker.com/get-started) e [Docker Compose](https://docs.docker.com/compose/) instalados em sua máquina.

## Configuração

### 1. Clonando o Repositório

Clone este repositório em sua máquina local:

````bash
$ git clone https://github.com/victorstochero/docker-setup.git
$ cd docker-setup
````
2. Configuração do Docker
Use o docker-compose para configurar e iniciar os serviços. Execute o seguinte comando na raiz do projeto:
````bash
$ docker-compose up -d --build
````

## Rodando PHP Puro
Para rodar PHP puro, adicione seus arquivos PHP na pasta app.

## Rodando WordPress
Para rodar um projeto WordPress:
````bash
$ docker-compose exec app bash #acessa o terminal do container app
$ cd app/public #Acesse a pasta public onde o WordPress será instalado
$ wp core download --allow-root #Use o WP-CLI para baixar a versão mais recente do WordPress
````
Se o Docker não exibir as pastas na IDE, reinicie os containers. <br>
Renomeie o arquivo `app/public/wp-config.php` para Configure o banco de dados no arquivo app/wp-config.php como abaixo, caso tenha alterado os dados no arquivo .env do projeto, coloque os dados corretos:
````.php
// ** Database settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'app_db' );

/** Database username */
define( 'DB_USER', 'user' );

/** Database password */
define( 'DB_PASSWORD', 'pass' );

/** Database hostname */
define( 'DB_HOST', 'mysql' );
````
O WordPress estará disponível em http://localhost.

## Rodando Laravel
Para rodar um projeto Laravel:
````bash
$ docker-compose exec app bash #acessa o terminal do container app
$ laravel new app -f #utilize o -f para forçar a instalação pois a pasta app já existe
````
Configure o banco de dados no arquivo app/.env como abaixo, caso tenha alterado os dados no arquivo .env do projeto, coloque os dados corretos:
````.env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=app_db
DB_USERNAME=user
DB_PASSWORD=pass
````

Se não estiver no container do app, acesse pelo comando abaixo:
````bash
$ docker-compose exec app bash #acessa o terminal do container app
````
Defina as permissões necessárias (dentro do container do app)
````bash
$ chown -R www-data:www-data /var/www/app/storage /var/www/app/bootstrap/cache
$ chmod -R 775 /var/www/app/storage /var/www/app/bootstrap/cache
````
Saia do container do app e entre no container do node:
````bash
$ exit
$ docker-compose exec node bash
````
Execute o servidor Laravel:
````bash
$ npm install && npm run dev
````
O Laravel estará disponível em http://localhost.

## Contribuições
Sinta-se à vontade para abrir issues ou pull requests. 
Todas as contribuições são bem-vindas!
