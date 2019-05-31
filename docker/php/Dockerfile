FROM php:fpm

RUN apt-get update -y --fix-missing \
    && apt-get install -y --no-install-recommends \
    libzip-dev \
    zlib1g-dev \
    && docker-php-ext-install \
    zip

# https://getcomposer.org/download/
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('sha384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

# https://getcomposer.org/doc/03-cli.md#composer-allow-superuser
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

RUN composer global require "laravel/installer"

RUN apt-get update -y --fix-missing \
    && apt-get install -y --no-install-recommends \
    libpq-dev \
    && docker-php-ext-install \
    pdo_mysql

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get update -y --fix-missing \
    && apt-get install -y --no-install-recommends nodejs

RUN pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable \
    redis

WORKDIR /src
