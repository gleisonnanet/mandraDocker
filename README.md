#  Mandra Docker
 
* PHP
* Apache
* MySQL
* phpMyAdmin
* Redis

No momento, temos várias versões diferentes de PHP. Use a versão php apropriada conforme necessário:

* 5.4.x
* 5.6.x
* 7.1.x
* 7.2.x
* 7.3.x
* 7.4.x
* 8.0.x

> Observe que simplificamos a estrutura do projeto de vários ramos para cada versão php, para um ramo mestre centralizado. Por favor, deixe-nos saber se você encontrar qualquer problema. 
##  Instalação
 
* Clone este repositório em seu computador local
* configure .env conforme necessário 
*Execute o `docker-compose up -d`.

```shell
git clone https://github.com/sprintcube/docker-compose-lamp.git
cd docker-compose-lamp/
cp sample.env .env
// modifique sample.env conforme necessário
docker-compose up -d
// Entre localhost
```

Sua pilha LAMP agora está pronta !! Você pode acessá-lo via `http://localhost`.

##  Configuração e uso

### Informações gerais
Este Docker Stack foi criado para desenvolvimento local e não para uso em produção.

### Configuração
Este pacote vem com opções de configuração padrão. Você pode modificá-los criando um arquivo `.env` em seu diretório raiz.
Para facilitar, basta copiar o conteúdo do arquivo `sample.env` e atualizar os valores das variáveis ​​de ambiente de acordo com sua necessidade.

### Variáveis ​​de Configuração
Existem as seguintes variáveis ​​de configuração disponíveis e você pode personalizá-las sobrescrevendo em seu próprio arquivo `.env`.

---
#### PHP
---
_**PHPVERSION**_
É usado para especificar qual versão do PHP você deseja usar. O padrão é sempre a versão mais recente do PHP.

_**PHP_INI**_
Defina sua modificação `php.ini` personalizada para atender aos seus requisitos.

---
#### Apache 
---

_**DOCUMENT_ROOT**_

É uma raiz de documento para o servidor Apache. O valor padrão para isso é `. / Www`. Todos os seus sites irão aqui e serão sincronizados automaticamente.

_**APACHE_DOCUMENT_ROOT**_

Valor do arquivo de configuração do Apache. O valor padrão para isso é /var/www/html.

_**VHOSTS_DIR**_

Isso é para hosts virtuais. O valor padrão para isso é `./Config/vhosts`. Você pode colocar seus arquivos conf de hosts virtuais aqui.

> Certifique-se de adicionar uma entrada ao arquivo `hosts` do seu sistema para cada host virtual.

_**APACHE_LOG_DIR**_

Isso será usado para armazenar logs do Apache. O valor padrão para isso é`./logs/apache2`.

---
#### Database
---

_**DATABASE**_
Defina qual versão do MySQL ou MariaDB você gostaria de usar.

_**MYSQL_DATA_DIR**_

Este é o diretório de dados do MySQL. O valor padrão para isso é `./data/mysql`. Todos os seus arquivos de dados MySQL serão armazenados aqui.

_**MYSQL_LOG_DIR**_

Isso será usado para armazenar logs do Apache. O valor padrão para isso é `./logs/mysql`.

## Web Server

Apache está configurado para rodar na porta 80. Então, você pode acessá-lo via `http://localhost`.

#### Apache Modules

Por padrão, os módulos a seguir estão habilitados.

* rewrite
* headers

> Se você quiser habilitar mais módulos, basta atualizar `./bin/webserver/Dockerfile`. Você também pode gerar um PR e nós faremos a fusão se parecer bom para uso geral.
>Você tem que reconstruir a imagem do docker executando `docker-compose build` e reinicie os contêineres do docker

#### Connect via SSH

Você pode se conectar ao servidor web usando `docker-compose exec` comando para executar várias operações nele. Use o comando abaixo para fazer login no container via ssh.

```shell
docker-compose exec webserver bash
```

## PHP

A versão instalada do php depende do seu arquivo `.env`.

#### Extensões

Por padrão, as seguintes extensões são instaladas.
Pode ser diferente para a versão do PHP <7.x.x

* mysqli
* pdo_sqlite
* pdo_mysql
* mbstring
* zip
* intl
* mcrypt
* curl
* json
* iconv
* xml
* xmlrpc
* gd

> Se você quiser instalar mais extensão, basta atualizar`./bin/webserver/Dockerfile`. Você também pode gerar um PR e nós faremos a fusão se parecer bom para uso geral.
> Você tem que reconstruir a imagem do docker executando `docker-compose build` e reinicie os contêineres do docker.

## phpMyAdmin

phpMyAdmin está configurado para ser executado na porta 8080. Use as seguintes credenciais padrão.

http://localhost:8080/  
username: root  
password: tiger

## Redis

Ele vem com o Redis. Ele roda na porta padrão`6379`.

## Contributing
Ficaremos felizes se você quiser criar uma solicitação de pull ou ajudar as pessoas com seus problemas. Se você deseja criar um PR, lembre-se de que esta pilha não foi construída para uso em produção e as alterações devem ser boas para uso geral e não muito especializadas.
> Observe que simplificamos a estrutura do projeto de vários ramos para cada versão php, para um ramo mestre centralizado. 
Por favor, crie seu PR no ramo mestre.
> 
Obrigado!

## Por que você não deve usar esta pilha sem modificações na produção
Queremos capacitar os desenvolvedores para criar aplicativos criativos rapidamente. Portanto, estamos fornecendo um ambiente de desenvolvimento local fácil de configurar para diversos Frameworks e versões de PHP.
Na produção, você deve modificar no mínimo os seguintes assuntos:

* manipulador php: mod_php=> php-fpm
* proteger usuários mysql com limitações de IP de origem adequadas
