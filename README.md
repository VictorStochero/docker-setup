# Ambiente de Desenvolvimento com Docker

Este repositório contém uma configuração de Docker para um ambiente de desenvolvimento que suporta PHP 8.3, NGINX, MySQL 8.0 e Node.js 23.0.0. Este projeto é ideal para desenvolvimento com Laravel, PHP puro ou WordPress.

## Estrutura do Projeto

A estrutura do projeto é a seguinte:
A pasta app é onde você deve colocar seus arquivos PHP. <br>
MySQL é onde os dados do banco de dados são armazenados. <br>
A pasta config contém os arquivos de configuração do NGINX e PHP.<br>
O arquivo .env contém as variáveis de ambiente para o Docker Compose.<br>
O arquivo docker-compose.yml contém a configuração do Docker Compose.<br>
O arquivo .gitignore contém os arquivos que não devem ser versionados. <br>


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
├── .env <br>
├── .gitignore <br>
└── docker-compose.yml
````


## Pré-requisitos

- [Docker](https://www.docker.com/get-started) e [Docker Compose](https://docs.docker.com/compose/) instalados em sua máquina.

## Configuração

### 1. Clonando o Repositório

Clone este repositório em sua máquina local:

````bash
git clone https://github.com/victorstochero/docker-setup.git
cd docker-setup
````
2. Configuração do Docker
Use o docker-compose para configurar e iniciar os serviços. Execute o seguinte comando na raiz do projeto:
````bash
docker-compose up -d
````

## Uso
### Rodando PHP Puro
Para rodar PHP puro, adicione seus arquivos PHP na pasta app.

### Rodando WordPress
Para rodar o WordPress, insira os arquivos do WordPress na pasta app.

### Rodando Laravel
Para rodar um projeto Laravel:

Crie um novo projeto Laravel:

````bash
$ docker exec app bash #acessa o terminal do container app
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
Defina as permissões necessárias:
````bash
chown -R www-data:www-data /var/www/app/storage /var/www/app/bootstrap/cache
chmod -R 775 /var/www/app/storage /var/www/app/bootstrap/cache
````

Execute o servidor Laravel:
````bash
php artisan serve --port=80
````
O Laravel estará disponível em http://localhost.

## Contribuições
Sinta-se à vontade para abrir issues ou pull requests. 
Todas as contribuições são bem-vindas!
