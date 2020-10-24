FROM php:7.3-fpm-alpine

MAINTAINER JG <julien@mangue.eu>

RUN apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        curl-dev \
        imagemagick-dev \
        libtool \
        libxml2-dev \
        postgresql-dev \
        sqlite-dev \
    && apk add --no-cache \
        curl \
        git \
        imagemagick \
        mysql-client \
        postgresql-libs \
        libintl \
        icu \
        icu-dev \
        libzip-dev \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && docker-php-ext-install \
        bcmath \
        curl \
        iconv \
        mbstring \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        pdo_sqlite \
        pcntl \
        tokenizer \
        xml \
        zip \
        intl \
    && curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && apk del -f .build-deps
###### Xdebug ######
RUN apk add --no-cache $PHPIZE_DEPS
RUN pecl install xdebug-2.9.3 \
    && docker-php-ext-enable xdebug \
&& echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
&& echo "xdebug.remote_autostart=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
&& echo "xdebug.remote_connect_back=off" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
&& echo "xdebug.remote_host=host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
&& echo "xdebug.remote_port=9005" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
&& echo "xdebug.idekey=PHPSTORM" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
&& echo "xdebug.max_nesting_level=1500" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
###### Xdebug ######
WORKDIR /var/www
