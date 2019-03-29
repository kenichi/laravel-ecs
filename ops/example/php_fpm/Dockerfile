FROM php:7.2-fpm-alpine

# replace www-data(82:82) with www-data(1000:1000)
ARG NAME=www-data
ENV NAME ${NAME}
RUN deluser www-data && \
    adduser -s /bin/sh -D -u 1000 -g '' ${NAME} ${NAME} && \
    chown -R ${NAME}:${NAME} /home/${NAME}

# needed packages
RUN apk add --no-cache autoconf g++ libtool make pcre-dev \
                       postgresql-dev \
                       zlib-dev

# install required php extensions
RUN docker-php-ext-install bcmath \
                           iconv \
                           opcache \
                           pdo pdo_pgsql pgsql \
                           zip

# opcache config
COPY opcache-recommended.ini /usr/local/etc/php/conf.d/

# laravel config
COPY laravel.ini /usr/local/etc/php/conf.d/
COPY xlaravel.pool.conf /usr/local/etc/php-fpm.d/

# clean
RUN apk del autoconf g++ libtool make pcre-dev
RUN rm -rf /tmp/* /var/cache/apk/*

# no USER is needed, since php will setuid
WORKDIR /var/www
CMD ["php-fpm"]
EXPOSE 9000
