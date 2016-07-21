FROM php:7.0-apache

RUN apt-get update -qq ; apt-get install -y -qq libxml2-dev unzip git \
  mysql-client \
  libpng12-dev libjpeg62-turbo-dev libfreetype6-dev imagemagick libmagick++-dev \
  ; pecl install imagick \
  ; docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  ; docker-php-ext-install pdo_mysql soap opcache gd bcmath \
  ; docker-php-ext-enable imagick \
  ; a2enmod rewrite ; service apache2 restart
COPY php.ini /usr/local/etc/php/

# Install composer
RUN curl -sS https://getcomposer.org/installer | php \
  ; mv composer.phar /usr/bin/composer \
; composer global require hirak/prestissimo

# Install drupal Console & drush
RUN curl https://drupalconsole.com/installer -L -o drupal.phar \
  ; mv drupal.phar /usr/local/bin/drupal \
  ; chmod +x /usr/local/bin/drupal ; drupal init --override \
  ; composer global require phing/phing drush/drush \
; ln -s ~/.composer/vendor/bin/* /usr/local/bin

# FE Tools
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
  ; apt-get install -y nodejs
