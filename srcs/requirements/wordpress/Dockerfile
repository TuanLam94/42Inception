FROM    debian:11.10

RUN     apt-get update \
        && apt-get install -y \
        wget \
        unzip \
        libpng-dev \
        libjpeg-dev \
        libfreetype6-dev \
        libzip-dev \
        php-fpm \
        php-mysql \
        php-gd \
        php-zip \
        php-pdo \
        php-mysqli \

RUN     docker-php-ext-configure gd \
            --with-freetype \
            --with-jpeg \
        && docker-php-ext-install gd \
        && docker-php-ext-install mysqli \
        && docker-php-ext-install zip \
        && docker-php-ext-install pdo pdo_mysql

RUN     wget https://wordpress.org/latest.tar.gz \
        && tar -xzvf latest.tar.gz \
        && mv wordpress