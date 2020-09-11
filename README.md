## Note

## nginx

[Laravel nginx.conf Example](https://laravel.com/docs/7.x/deployment#nginx)

[NGINX - Pitfalls and Common Mistakes](https://www.nginx.com/resources/wiki/start/topics/tutorials/config_pitfalls/)

### php

```sh
# allocate php.ini
php --ini

# list php module
php -m

# phpinfo() from cmd
php -i
```

### php-fpm

```sh
# allocate php-fpm.conf (man php-fpm)
php-fpm -tt
```

Though `user` directive, [which set the user of FPM processes](https://www.php.net/manual/en/install.fpm.configuration.php)
is mandatory for php-fpm. It's used for php-fpm as a service.
By execute `php-fpm` directly, the process owner is the executor.

### Docker

MySQL container creates a [anonymous volume](https://github.com/docker-library/mysql/issues/255)(`/var/lib/mysql`).
Though normally all of us do bind for persisting data, in case we didn't,
recreating mysql container leaves lots of unused volumes.

Use [_.dockerignore_](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#exclude-with-dockerignore)
to prevent irrelevant files be copied to docker image while building.

#### Dockerfile

Each command in _Dockerfile_ can be cached sequentially. To benefit from
the cache mechanism, put commands foremost that:

1. May not be changed frequently
2. Most time consuming

## Question

- [nginx] Don't know why append `$query_string` to index.php