FROM php:5.6-fpm

MAINTAINER aleksandr.sokol@teqspring.net <asokol>

ENV PATH $PATH:/root/.composer/vendor/bin

# PHP extensions come first, as they are less likely to change between Yii releases
RUN apt-get update \
    && apt-get -y install \
            git \
            g++ \
            libicu-dev \
            libmcrypt-dev \
            zlib1g-dev \
        --no-install-recommends \

    # Install PHP extensions
    && docker-php-ext-install intl \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install zip \

    && apt-get purge -y g++ \
    && apt-get autoremove -y \
    && rm -r /var/lib/apt/lists/* \

    # Don't clear our valuable environment vars in PHP
    && echo "\nclear_env = no" >> /usr/local/etc/php-fpm.conf \

    # Fix write permissions with shared folders
    && usermod -u 1000 www-data
