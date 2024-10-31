FROM php:8.2-fpm

# Use the script to install PHP extensions for Debian-based images
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

# Install PHP extensions
RUN apt-get update && apt-get install -y \
    default-mysql-client \
    libicu-dev \
    libzip-dev \
    libxslt-dev \
    git \
    unzip \
    netcat-openbsd \
    && rm -rf /var/lib/apt/lists/*

RUN chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions mysqli pdo pdo_mysql gd curl xsl mbstring openssl zip soap bcmath intl sockets

RUN echo 'memory_limit = 4096M' >> /usr/local/etc/php/conf.d/docker-php-memlimit.ini;

RUN groupadd -g 1000 wordpress
RUN usermod -aG wordpress www-data

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer