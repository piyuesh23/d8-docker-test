FROM php:7.1.2-apache

RUN apt-get update -y && apt-get install -y libpng-dev
RUN apt-get update && apt-get install -y zlib1g-dev
RUN apt-get update && apt-get install -y cifs-utils
RUN docker-php-ext-install pdo pdo_mysql json gd mbstring opcache zip

RUN apt-get update && apt-get install --no-install-recommends --assume-yes --quiet ca-certificates curl git && rm -rf /var/lib/apt/lists/*
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail
RUN echo 'sendmail_path = /usr/bin/mhsendmail --smtp-addr mailhog:1025' > /usr/local/etc/php/php.ini


RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer && ln -s /root/.composer/vendor/bin/drush /usr/local/bin/drush

# Install Drush
RUN composer global require drush/drush:8.* && composer global update

COPY . /var/www/monjin
COPY .docker/php/vhosts.conf /etc/apache2/sites-available/000-default.conf

RUN chown -R www-data:www-data /var/www/monjin && a2enmod rewrite

# Mount CIFS
