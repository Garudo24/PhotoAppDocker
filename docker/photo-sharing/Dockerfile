FROM php:7.4.3-apache-buster

COPY ./apache/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY ./php/php.ini /usr/local/etx/php/php.ini

RUN set -x \
    && apt-get -y update \
    && apt-get install -y zip unzip git \
    && docker-php-ext-install pdo_mysql \
    && pecl install redis-5.1.1 \
    && docker-php-ext-enable redis

RUN set -x \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"

RUN set -x \
    && a2enmod rewrite

EXPOSE 80