FROM php:7.2-fpm
#COPY conf/php.ini /usr/local/etc/php/

RUN set -x \
    && apt-get update \
    && apt-get install -y zlib1g-dev mariadb-client \
    && docker-php-ext-install zip mysqli pdo_mysql \
    && pecl install xdebug

#Composer install
RUN set -x \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

WORKDIR /var/www

RUN set -x \
    && composer global require "laravel/installer"