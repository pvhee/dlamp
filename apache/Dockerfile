FROM debian:stretch

MAINTAINER Saphyel <Saphyel@gmail.com>

RUN apt update ; apt install -y ca-certificates unzip curl apache2 \
    libapache2-mod-php imagemagick php7.0-mbstring php7.0-dev php7.0-gd \
    php7.0-intl php-imagick php7.0-soap php7.0-bcmath php-xdebug php7.0-curl \
    php7.0-mysql --fix-missing ; rm -rf /var/lib/apt/lists
RUN a2enmod rewrite ; service apache2 start
ADD 000-default.conf /etc/apache2/sites-available/000-default.conf

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php \
  ; mv composer.phar /usr/bin/composer \
  ; ln -s /root/.composer/vendor/bin/* /usr/local/bin
; composer global require hirak/prestissimo

# Install drupal Console & drush
RUN curl https://drupalconsole.com/installer -L -o drupal.phar \
  ; mv drupal.phar /usr/local/bin/drupal \
; chmod +x /usr/local/bin/drupal ; drupal init --override 

RUN chown www-data /var/www
CMD /usr/sbin/apache2ctl -D FOREGROUND
