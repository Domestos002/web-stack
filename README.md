# Web stack

> Basic web stack for web developers

Docker-compose script what runs web application stack with few command lines!

|Service|Description|
|-|-|
|[nginx](https://hub.docker.com/_/nginx "nginx on docker hub")|Nginx web server|
|[httpd](https://hub.docker.com/_/httpd "httpd on docker hub")|Apache web server|
|[php-fpm](https://hub.docker.com/_/php "php-fpm on docker hub")|PHP FPM version|
|[mariadb](https://hub.docker.com/_/mariadb "mariadb on docker hub")|MariaDB database|
|[mysql](https://hub.docker.com/_/mysql "mysql on docker hub")|MySQL database|
|[mongo](https://hub.docker.com/_/mongo "mongo on docker hub")|Document database|
|[express](https://www.npmjs.com/package/express-generator "express-generator on npm")|Basic NodeJS Express application template|
|[strapi](https://github.com/strapi/strapi "strapi on github")|open-source headless CMS to build powerful APIs with no effort|
|\**[adminer](https://hub.docker.com/_/adminer "adminer on docker hub")*|Simple SQL database management Web UI|
|\**[mongo-express](https://hub.docker.com/_/mongo-express "mongo-express on docker hub")* |Simple document database management Web UI|

\* *optional service*

# Installation

```bash
git clone https://github.com/disaipe/web-stack.git my-site
cd my-site
```

# Usage example

Before working create and [edit](#configure) `.env` file
```bash
cp .env.example .env
```

#### LEMP (nginx + php-fpm + mariadb)
1. Check [configuration files](#configuration-files) if needed
2. Start services
```bash
docker-compose up -d lemp
```

#### LAMP (httpd + php-fpm + mariadb)
1. Check [configuration files](#configuration-files) if needed
2. Start services
```bash
docker-compose up -d lamp
```

#### NodeJS Express template

Basic Express application based on [express-generator](https://www.npmjs.com/package/express-generator) with support view and stylesheet engines.
By default it deploys with **pug** and **sass** engines.

1. Open `docker-compose.yml` and configure *express* service, if you want:
    - *EXPRESS_VIEW_ENGINE* - view engine (dust|ejs|hbs|hjs|jade|pug|twig|vash)
    - *EXPRESS_STYLE_ENGINE* - stylesheet support (less|stylus|compass|sass)
2. Run application service:
```bash
docker-compose up -d express
```

#### Optional services
To start optional service, e.g. *adminer* (it will be available on http://hostname:8081 by default)
```bash
docker-compose up -d adminer
```

# Predefined CMS

You can to install some CMS very fast and very easy - just switch to CMS branch and start installation script:
```bash
git checkout bitrix
./install.sh
```

Supported CMS:
- [x] [Bitrix](https://www.1c-bitrix.ru/)
- [x] [Evolution CMS](https://evo.im/)
- [x] [Wordpress](https://wordpress.org/)

# Configure
By default, stack are ready  to basic work, but you can edit your configuration for each service.


### Compose environment

Environment file helps to configure services base options:
- APP_NAME - application name, uses as prefix for services containers names
- HTTP_PORT - public port for chosen web server
- HTTP_HOST - hostname for web servers internal usage
- HTTPD_VERSION - httpd version from hub tags (*latest* as default)
- PHP_VERSION - php version from hub tags
- NODE_VERSION - NodeJS version from hub tags
- MYSQL_VERSION - mysql version from hub tags
- MYSQL_ROOT_PASSWORD - default root password for mariadb
- MYSQL_DATABASE - database name
- MYSQL_USER - database user name
- MYSQL_PASSWORD - database user password
- MARIADB_VERSION - mariadb version from hub tags
- MARIADB_ROOT_PASSWORD - default root password for mariadb
- MARIADB_DATABASE - database name
- MARIADB_USER - database user name
- MARIADB_PASSWORD - database user password
- MONGODB_VERSION - mongodb version from hub tags
- MONGODB_ROOT_USERNAME - mongodb username
- MONGODB_ROOT_PASSWORD - mongodb user password
- MONGODB_DATABASE - mongodb database name
- MONGODB_USERNAME - non-root user name
- MONGODB_PASSWORD - non-root user password
- MONGODB_EXPRESS_PORT - public port for mongo-express
- ADMINER_PORT - public port for adminer
- STRAPI_PORT - public Strapi port

If you changes environment after service start, you need stop and rebuild changed containers, e.g.:
```bash
docker-compose stop
docker-compose rm php
docker-compose build php
docker-compose start -p lemp
```

### Configuration files
You can edit services configuration files as you wish.

After changes you need restart changed containers, e.g.:
```bash
docker-compose stop
docker-compose restart nginx
```

|Service|Configuration files|
|-|-|
|nginx|etc/nginx/conf.d/default.conf|
|httpd|etc/httpd/httpd.conf<br>etc/httpd/conf.d/vhosts.conf|
|php|etc/php/php.ini|
|mariadb|etc/mariadb/conf.d/default.cnf|
