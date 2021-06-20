# docker build . -t kelly4286/php:8.0-fpm
# docker push kelly4286/php:8.0-fpm
FROM php:8.0-fpm

WORKDIR /account_book/dev

RUN apt-get update \
  && apt-get install -my gnupg unzip \
  && apt-get -y --no-install-recommends install locales apt-transport-https \
  && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
  && locale-gen \
  && apt-get -y install fonts-wqy-microhei ttf-wqy-microhei fonts-wqy-zenhei ttf-wqy-zenhei \
  && apt-get -y --no-install-recommends install unixodbc-dev zlib1g-dev libpng-dev \
  && pecl install xdebug \
  && docker-php-ext-enable xdebug  \
  && docker-php-ext-install gd mysqli pdo pdo_mysql \
  && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php composer-setup.php \
  && php -r "unlink('composer-setup.php');" \
  && mv composer.phar /usr/local/bin/composer \
  && curl -fsSL https://deb.nodesource.com/setup_16.x | bash -\
  && apt-get install -y nodejs\
  && pecl clear-cache \
  && docker-php-source delete \
  && rm -rf /var/lib/apt/lists /tmp/pear \
  && docker-php-source delete \
  && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false
