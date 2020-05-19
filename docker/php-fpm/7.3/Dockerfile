FROM php:7.3-fpm-alpine
WORKDIR /application

RUN echo "Install packages +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk update && \
    apk add --no-cache musl m4 libbz2 perl autoconf pkgconf dpkg-dev dpkg libmagic file libgcc libstdc++ binutils gmp isl libgomp \
    libatomic mpfr4 mpc1 gcc musl-dev libc-dev g++ make re2c musl-utils && \
    echo "Install extention ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    docker-php-ext-install -j$(nproc) opcache && \
    apk add --no-cache postgresql-dev && \
    docker-php-ext-install -j$(nproc) pdo_pgsql && \
    docker-php-ext-install -j$(nproc) pgsql && \
    docker-php-ext-install -j$(nproc) pdo_mysql && \
    docker-php-ext-install -j$(nproc) mysqli && \
    apk add --no-cache libzip-dev && \
    docker-php-ext-install -j$(nproc) zip && \
    apk add --no-cache imap-dev bzip2-dev && \
    docker-php-ext-install -j$(nproc) bz2 && \
    docker-php-ext-install -j$(nproc) bcmath && \
    apk add --no-cache icu-dev && \
    docker-php-ext-install -j$(nproc) intl && \
    apk add --no-cache gettext-dev && \
    docker-php-ext-install -j$(nproc) gettext && \
    apk add --no-cache freetype-dev libjpeg-turbo-dev libpng-dev libwebp-dev && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    --with-png-dir=/usr/include/ --with-webp-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd && \
    apk add --no-cache imap-dev openssl-dev krb5-dev && \
    PHP_OPENSSL=yes docker-php-ext-configure imap --with-imap --with-imap-ssl --with-kerberos && \
    docker-php-ext-install -j$(nproc) imap && \
    docker-php-ext-install -j$(nproc) calendar && \
    docker-php-ext-install -j$(nproc) exif && \
    apk add --no-cache openldap-dev && \
    docker-php-ext-install -j$(nproc) ldap && \
    apk add --no-cache libxml2-dev && \
    docker-php-ext-install -j$(nproc) soap && \
    docker-php-ext-install -j$(nproc) sockets && \
    docker-php-ext-install -j$(nproc) xmlrpc && \
    apk add --no-cache tidyhtml-dev && \
    docker-php-ext-install -j$(nproc) tidy && \
    echo "Remove packages ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk del autoconf m4 dpkg-dev perl dpkg file g++ gcc binutils libatomic libgomp libc-dev musl-dev make pkgconf \
    re2c libbz2 libmagic libstdc++ libgcc mpc1 mpfr4 isl gmp && \
    rm -rf /var/cache/apk/*

RUN echo "Install packages +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk update && \
    apk add --no-cache musl m4 libbz2 perl autoconf pkgconf dpkg-dev dpkg libmagic file libgcc libstdc++ binutils gmp isl libgomp \
    libatomic mpfr4 mpc1 gcc musl-dev libc-dev g++ make re2c musl-utils && \
    echo "Install PECL extention +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    pecl install psr && \
    docker-php-ext-enable psr && \
    pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    apk add --no-cache zlib-dev libmemcached-dev cyrus-sasl-dev && \
    pecl install memcached && \
    docker-php-ext-enable memcached && \
    apk add --no-cache libmcrypt-dev && \
    pecl install mcrypt && \
    docker-php-ext-enable mcrypt && \
    pecl install mongodb && \
    docker-php-ext-enable mongodb && \
    pecl install redis && \
    docker-php-ext-enable redis && \
    apk add --no-cache unixodbc-dev && \
    pecl install sqlsrv && \
    docker-php-ext-enable sqlsrv && \
    pecl install pdo_sqlsrv && \
    docker-php-ext-enable pdo_sqlsrv && \
    apk add --no-cache imagemagick-dev && \
    pecl install imagick && \
    docker-php-ext-enable imagick && \
    pecl clear-cache && \
    echo "Remove packages ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk del autoconf m4 dpkg-dev perl dpkg file g++ gcc binutils libatomic libgomp libc-dev musl-dev make pkgconf \
    re2c libbz2 libmagic libstdc++ libgcc mpc1 mpfr4 isl gmp && \
    rm -rf /var/cache/apk/*

ENV PHALCON_VERSION=4.0.6
RUN echo "Install packages +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk update && \
    apk add --no-cache musl m4 libbz2 perl autoconf pkgconf dpkg-dev dpkg libmagic file libgcc libstdc++ binutils gmp isl libgomp \
    libatomic mpfr4 mpc1 gcc musl-dev libc-dev g++ make re2c musl-utils && \
    echo "Install Phalcon ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    set -xe && \
    curl -LO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz && \
    tar xzf v${PHALCON_VERSION}.tar.gz && \
    cd cphalcon-${PHALCON_VERSION}/build && \
    sh install && \
    echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini && \
    cd ../.. && \
    rm -rf v${PHALCON_VERSION}.tar.gz cphalcon-${PHALCON_VERSION} && \
    echo "Remove packages ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk del autoconf m4 dpkg-dev perl dpkg file g++ gcc binutils libatomic libgomp libc-dev musl-dev make pkgconf \
    re2c libbz2 libmagic libstdc++ libgcc mpc1 mpfr4 isl gmp && \
    rm -rf /var/cache/apk/*

RUN echo "Install packages +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk update && \
    apk add --no-cache musl m4 libbz2 perl autoconf pkgconf dpkg-dev dpkg libmagic file libgcc binutils gmp isl libgomp \
    libatomic mpfr4 mpc1 gcc musl-dev libc-dev g++ make re2c musl-utils && \
    echo "Install Swoole +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    pecl install swoole && \
    docker-php-ext-enable swoole && \
    pecl clear-cache && \
    echo "Remove packages ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk del autoconf m4 dpkg-dev perl dpkg file g++ gcc binutils libatomic libgomp libc-dev musl-dev make pkgconf \
    re2c libbz2 libmagic libgcc mpc1 mpfr4 isl gmp && \
    rm -rf /var/cache/apk/*

COPY ./php.ini /usr/local/etc/php/php.ini
