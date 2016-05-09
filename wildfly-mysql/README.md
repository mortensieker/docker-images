# Wildfly with MySQL
A Wildfly application container that uses a MySQL database.

Inspired by Arun Guptas [wildfly-mysql-javaee7](https://github.com/arun-gupta/docker-images/tree/master/wildfly-mysql-javaee7), with a few modifications.

Run this using [docker-compose](https://docs.docker.com/compose/) to ease the configuration of multiple containers.

I have added the support for enabling the wildfly admin console.
Simply add the ```- ENABLE_ADMIN=on``` in the environments section to enable the admin console.

```
mysqldb:
  container_name: "db"
  image: mysql:latest
  environment:
    MYSQL_DATABASE: datasource
    MYSQL_USER: mysql
    MYSQL_PASSWORD: mysql
    MYSQL_ROOT_PASSWORD: supersecret
mywildfly:
  image: sieker/wildfly-mysql
  container_name: mywildfly
  environment:
    - MYSQL_URI=db:3306
    - ENABLE_ADMIN=on
  links:
    - mysqldb:db
  ports:
    - "8080:8080"
    - "9990:9990"
```
