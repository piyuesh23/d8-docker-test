FROM php:7.1.2-apache

RUN apt-get update -y && apt-get install -y libpng-dev
RUN apt-get update && apt-get install -y zlib1g-dev
RUN docker-php-ext-install pdo pdo_mysql json gd mbstring opcache

COPY . /var/www/monjin
COPY .docker/php/vhosts.conf /etc/apache2/sites-available/000-default.conf

RUN chown -R www-data:www-data /var/www/monjin && a2enmod rewrite
