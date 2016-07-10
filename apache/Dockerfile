FROM php:7.0-apache

RUN apt-get update && apt-get install -y git curl ca-certificates libfreetype6-dev unzip acl libxml2-dev libicu-dev \
  && docker-php-ext-install soap intl gd bcmath mbstring mysqli opcache curl \
 && rm -rf /var/lib/apt/lists/* && apt-get purge --auto-remove -y

RUN a2enmod rewrite
ADD 000-default.conf /etc/apache2/sites-available/000-default.conf
RUN sed -i "s/^;always_populate_raw_post_data = -1$/always_populate_raw_post_data = -1/" /usr/src/php/php.ini \
  && sed -i "s/^;phar.readonly = On$/phar.readonly = On/" /usr/src/php/php.ini \
  && sed -i "s/^;date.timezone =$/date.timezone = \"Europe\/London\"/" /usr/src/php/php.ini \
&& sed -i "s/^allow_url_fopen = On$/allow_url_fopen = Off/" /usr/src/php/php.ini

# Install composer
RUN curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/bin/composer \
&& composer global require hirak/prestissimo

RUN curl https://drupalconsole.com/installer -L -o drupal.phar \
  && mv drupal.phar /usr/local/bin/drupal \
&& chmod +x /usr/local/bin/drupal && drupal init --override

# Ensure that the production container will run with the www-data user
RUN chown www-data /var/www/html

# Install dependencies
# RUN composer install -o
# php-imagick php-xdebug OPcode php7.0-curl
