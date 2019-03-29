# laravel-ecs example config

[Read More](https://medium.com/phylos/leaving-the-forge-part-1)

```
$ cd ops/
$ docker-compose build
...
$ docker-compose up -d
...
$ docker-compose exec example_php_fpm /bin/sh -c \
   'curl -L -o install_composer.php https://getcomposer.org/installer && \
    php install_composer.php --install-dir=/usr/local/bin --filename=composer && \
    cd /var/www/example && \
    composer install'
...
$ sudo sh -c "echo '127.0.0.1 example.test' >> /etc/hosts"
```
