FROM php:7.4-fpm
LABEL maintainer="Khary Sharpe <ksharpe@email.com>"

ARG XDEBUG_HOST="docker.for.mac.localhost"
ARG XDEBUG_CONF="disabled"

ENV LANGUAGE   en_US.UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8
ENV COMPOSER_ALLOW_SUPERUSER 1

# Ensure UTF-8
RUN DEBIAN_FRONTEND="noninteractive" apt-get clean && apt-get update
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y apt-utils locales
RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "LANG=en_US.UTF-8" > /etc/locale.
RUN DEBIAN_FRONTEND="noninteractive" locale-gen en_US.UTF-8

# Install system dependencies
RUN apt-get update && apt-get install -y \
    vim \
    curl \
    wget \
    build-essential \
    git \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    zip \
    unzip \
    libpq-dev

# Install node
RUN DEBIAN_FRONTEND="noninteractive" curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y nodejs    

# Install PHP extensions
RUN docker-php-ext-install -j$(nproc) opcache bcmath zip pdo_pgsql pgsql 
#    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
#    && docker-php-ext-install -j$(nproc) gd

# Install XDEBUG
RUN pecl install xdebug
RUN mkdir -p /usr/local/etc/php/${XDEBUG_CONF}
RUN \
    echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20160303/xdebug.so" > /usr/local/etc/php/${XDEBUG_CONF}/xdebug.ini && \
    echo "xdebug.default_enable = 1" >> /usr/local/etc/php/${XDEBUG_CONF}/xdebug.ini && \
    echo "xdebug.remote_enable = 1" >> /usr/local/etc/php/${XDEBUG_CONF}/xdebug.ini && \
    echo "xdebug.remote_handler = dbgp" >> /usr/local/etc/php/${XDEBUG_CONF}/xdebug.ini && \
    echo "xdebug.remote_autostart = 0" >> /usr/local/etc/php/${XDEBUG_CONF}/xdebug.ini && \
    echo "xdebug.remote_connect_back = 0" >> /usr/local/etc/php/${XDEBUG_CONF}/xdebug.ini && \
    echo "xdebug.remote_port = 9000" >> /usr/local/etc/php/${XDEBUG_CONF}/xdebug.ini && \
    echo "xdebug.remote_host =" ${XDEBUG_HOST} >> /usr/local/etc/php/${XDEBUG_CONF}/xdebug.ini && \
    echo "xdebug.profiler_enable=0" >> /usr/local/etc/php/${XDEBUG_CONF}/xdebug.ini && \
    echo "xdebug.profiler_enable_trigger=1" >> /usr/local/etc/php/${XDEBUG_CONF}/xdebug.ini && \
    echo "xdebug.profiler_output_dir=\"/tmp\"" >> /usr/local/etc/php/${XDEBUG_CONF}/xdebug.ini

# Install composer
COPY --from=composer:1.6 /usr/bin/composer /usr/bin/composer

##############################################################################
# phpunit
##############################################################################

ENV PHPUNIT_VERSION 9.4.2
RUN mkdir -p /root/src \
    && cd /root/src \
    && wget https://phar.phpunit.de/phpunit-${PHPUNIT_VERSION}.phar \
    && chmod +x phpunit-${PHPUNIT_VERSION}.phar \
    && mv phpunit-${PHPUNIT_VERSION}.phar /usr/local/bin/phpunit \
    && rm -rf /root/src \
    && phpunit --version


COPY ./resources/config/log.conf /usr/local/etc/php-fpm.d/zz-log.conf

COPY ./resources/config/php.ini-development /usr/local/etc/php/php.ini

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 3000
EXPOSE 3001
