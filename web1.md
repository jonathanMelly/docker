# Environnement docker (démarrer docker desktop) WEB
## NET (réseau)
```shell
docker network create web
```
## WEB (html + php)
```shell
cd ANY_PROJECT_DIRECTORY
docker run -itd --name web --net web --mount type=bind,src=%cd%,dst=/var/www/html/ -p 8080:80 php:8.1-apache
docker exec –it web docker-php-ext-install pdo pdo_mysql mysqli
docker exec –it web apachectl graceful
```
## DB

### Connect existing container
With an existing db container, you may connect it to the created network:

```shell
docker network connect web YOUR_OTHER_EXISTING_CONTAINER
```
**replace YOUR_OTHER_EXISTING_CONTAINER with it’s name, for instance "db" **

### Create new container
If you don’t already have a db container, you may create one:
```shell
docker run --name mariadb --net web --detach --env MARIADB_ROOT_PASSWORD=123 -p3306:3306 -v mariadb:/var/lib/mysql mariadb:10.3.34
```
