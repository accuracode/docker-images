ARG BASE_TAG

FROM php:${BASE_TAG}

ENV \
        PATH=/var/www/html:/var/www/html/vendor/bin:$PATH \
        TERM=linux \
        PHP_IDE_CONFIG=serverName=docker

COPY --from=mlocati/php-extension-installer:latest /usr/bin/install-php-extensions /usr/bin/

RUN apk add --no-cache \
        bash \
        nano

RUN install-php-extensions \
        amqp \
        soap \
        zip \
        bcmath \
        exif \
        gd \
        intl \
        opcache \
        pdo_mysql \
        pdo_pgsql \
        redis \
        imagick \
        sockets \
        rdkafka \
        imagick \
        xdebug

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"  && \
        echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/99-xdebug.ini && \
        echo "xdebug.client_host=host.docker.internal" >> /usr/local/etc/php/conf.d/99-xdebug.ini && \
        echo "xdebug.start_with_request=yes" >> /usr/local/etc/php/conf.d/99-xdebug.ini

WORKDIR /var/www/html

RUN chown -R www-data:www-data /var/www/html
