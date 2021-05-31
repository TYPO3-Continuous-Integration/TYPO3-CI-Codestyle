FROM composer:2
FROM bash:5
FROM php:7.4-alpine

COPY Build/entrypoint.sh /entrypoint.sh
COPY Configuration/.php_cs.php /.php_cs.php

COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY --from=bash /usr/local/bin/bash /usr/bin/bash

RUN apk update && apk upgrade \
    && apk add bash git libxml2-dev libzip-dev zip unzip curl \
    && rm -rf /var/cache/apk/*

RUN docker-php-ext-install zip

RUN echo -e "Install friendsofphp/php-cs-fixer" \
    && composer global require friendsofphp/php-cs-fixer --prefer-dist --no-progress \
    && ln -nfs /root/.composer/vendor/bin/php-cs-fixer /usr/bin/php-cs-fixer \
    && chmod a+x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
