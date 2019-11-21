FROM php:7.3-apache

RUN apt-get update

# Install tools required for build stage
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq \
    bash curl wget rsync ca-certificates openssl ssh git tzdata openntpd \
    libxrender1 fontconfig libc6 \
    mariadb-client gnupg binutils-gold autoconf \
    g++ gcc gnupg libgcc1 linux-headers-amd64 make python

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
 && chmod 755 /usr/bin/composer

# Install additional PHP libraries
RUN docker-php-ext-install bcmath pdo_mysql

# Install libraries for compiling GD, then build it
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq \
    libfreetype6-dev libpng-dev libjpeg-dev libpng-dev libjpeg-turbo-progs \
 && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
 && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
 && docker-php-ext-install -j${NPROC} gd

# Add ZIP archives support
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq \
    zlib1g-dev libzip-dev \
 && docker-php-ext-install zip

# Install xdebug
RUN pecl install xdebug-2.7.2 \
 && docker-php-ext-enable xdebug

# Enable XDebug
ADD xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

WORKDIR /app
