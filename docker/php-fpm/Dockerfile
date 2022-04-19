FROM php:7.3-fpm

#ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get -yq install \
        gnupg2 && \
    apt-get -y install \
            apt-utils \
            sed \
            g++ \
            git \
            lsof \
            default-mysql-client \
            curl \
            ssh \
            wget \
            imagemagick \
            libcurl3-dev \
            libicu-dev \
            libfreetype6-dev \
            libwebp-dev \
            libjpeg-dev \
            libjpeg62-turbo-dev \
            libonig-dev \
            libmagickwand-dev \
            libpq-dev \
            p7zip-full \
            libpng-dev libxpm-dev \
            libmcrypt-dev \
            libxml2-dev \
            libc-client-dev \
            libkrb5-dev \
            lame \
            procps \
            systemd \
            libzip-dev \
            zlib1g-dev \
            unzip \
            gzip \
            bzip2 \
            libcurl4-openssl-dev \
            libssl-dev && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
        sed -i 's/DEFAULT@SECLEVEL=2/DEFAULT@SECLEVEL=1/g' /etc/ssl/openssl.cnf

ARG X_LEGACY_GD_LIB=1
RUN if [ $X_LEGACY_GD_LIB = 1 ]; then \
        docker-php-ext-configure gd \
                --with-freetype-dir=/usr/include/ \
                --with-png-dir=/usr/include/ \
                --with-jpeg-dir=/usr/include/; \
    else \
        docker-php-ext-configure gd \
                --with-freetype=/usr/include/ \
                --with-jpeg=/usr/include/; \
    fi && \
    docker-php-ext-configure bcmath && \
    docker-php-ext-install \
        soap \
        zip \
        curl \
        bcmath \
        exif \
        gd \
        iconv \
        intl \
        mbstring \
        opcache \
        pdo_mysql  && \
    docker-php-ext-enable \
        soap \
        zip \
        curl \
        bcmath \
        exif \
        gd \
        iconv \
        intl \
        mbstring \
        opcache \
        pdo_mysql

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- \
        --filename=composer \
        --install-dir=/usr/local/bin \
        && chmod +x /usr/local/bin/composer
VOLUME /app
WORKDIR /app
