FROM php:7.3.6-fpm-alpine3.9

ARG PROJECT_ROOT_PATH

RUN apk upgrade --update && apk --no-cache add \
    bash \
    mc \
    nano \
    vim \
    coreutils \
    libltdl \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    postgresql-dev \
    icu-dev \
    openssh-client \
    postgresql-client \
    bash \
    git \
    binutils \
    openssl \
    unrar \
    libmcrypt-dev \
    libxslt-dev

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apk add --no-cache --virtual .tmp-deps \
    g++ \
    $PHPIZE_DEPS \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd pdo_mysql pdo_pgsql pgsql bcmath xsl soap intl

#ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data
#COPY fpm.conf /usr/local/etc/php-fpm.d/www.conf
COPY site.ini /usr/local/etc/php/conf.d/site.ini

WORKDIR ${PROJECT_ROOT_PATH}