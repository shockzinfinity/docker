Docker
=============

A repo to house my trusted Docker builds, see my [Docker Index Profile](https://index.docker.io/u/russmckendrick/) for more information.

## General Containers

- [Base](https://registry.hub.docker.com/u/russmckendrick/base/) - Base build for use with other Docker builds
- [NGINX Proxy](https://registry.hub.docker.com/u/russmckendrick/nginx-proxy/) - A reverse proxy container

## CentOS 7 LEMP Stack

- [NGinx & PHP 5.4](https://registry.hub.docker.com/u/russmckendrick/nginx-php/) - An all in-one NGINX / PHP container
- [MariaDB 5.5](https://registry.hub.docker.com/u/russmckendrick/mariadb/) - A MariaDB 5.5 container, best used with other containers
- [NGINX](https://registry.hub.docker.com/u/russmckendrick/nginx/) - Runs NGINX, designed to be run alongside a [PHP-FPM container](https://registry.hub.docker.com/u/russmckendrick/php-fpm/)
- [PHP 5.4 & PHP-FPM](https://registry.hub.docker.com/u/russmckendrick/php-fpm/)- Runs PHP 5.4 and PHP-FPM, for use with a [NGINX Container](https://registry.hub.docker.com/u/russmckendrick/nginx/)

To run a stack you would run something like;

```
docker run -d -v /home/containers/database:/var/lib/mysql --name="database" russmckendrick/mariadb
docker run -d -v /home/containers/web:/var/www/html --name="php" --link database:db russmckendrick/php-fpm
docker run -d -p 80 -v /home/containers/web:/var/www/html -e VIRTUAL_HOST=some.domain.com --link php:php-fpm --name="nginx" russmckendrick/nginx
```

See [this terminal session](https://asciinema.org/a/11731) for a demo or this [blog post](https://media-glass.es/2014/08/31/docker-fig-reverse-proxy-centos7/) for more details.
