# Laravel + Nginx + MySQL + Redis Docker Template

This is a Docker template that provides an environment with Laravel, Nginx, MySQL and Redis.

## Requirement

- [Docker](https://www.docker.com/)
  - docker-compose

## Usage

Run server:

```console
$ docker-compose up
```

Go to `http://localhost` and you'll see the website.

## Install

Clone repository:

```console
$ git clone https://github.com/PiroHiroPiro/docker_template_laravel_nginx_mysql_redis.git
$ cd docker_template_laravel_nginx_mysql_redis
```

Copy env files:

```console
$ cp ./docker/php/.env.example ./docker/php/.env
$ cp ./docker/mysql/.env.example ./docker/mysql/.env
```

Enter the database name and root user password in the copied env files `./docker/php/.env` and `./docker/mysql/.env`:

Create new Laravel application:

```console
$ docker-compose exec php laravel new [YOUR APPLICATION NAME]
```

Change project name:

```./docker/nginx/conf/default.conf
...
root /src/[YOUR APPLICATION NAME]/public;
...
```

Build images:

```console
$ docker network create laravel_network
$ docker-compose build
```

## Licence

This software is released under the MIT License, see [LICENSE](https://github.com/PiroHiroPiro/docker_template_laravel_nginx_mysql_redis/blob/master/LICENSE).

## Author

[Hiroyuki Nishizawa](https://github.com/PiroHiroPiro)
