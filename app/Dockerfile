FROM php:5.6.31-apache

RUN apt-get update && apt-get install -y \
       curl \
       unzip \
       apt-utils \
       zlib1g-dev \
       libpng12-dev \
       libmcrypt-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-source extract \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo pdo_mysql \
    && docker-php-ext-install zip \
    && docker-php-ext-install gd \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install opcache
RUN a2enmod rewrite

WORKDIR /tmp
RUN curl -LO https://www.cubecart.com/download/CubeCart-6.1.12.zip \
    && unzip CubeCart-6.1.12.zip -d cubecart \
    && rm -f CubeCart-6.1.12.zip \
    && rm -rf /var/www/html \
    && mv cubecart /var/www/html \
    && cd /var/www/html \
    && chown -R www-data:www-data /var/www/html

RUN echo '[Date]' > /usr/local/etc/php/conf.d/timezone.ini \
 && echo 'date.timezone = "Asia/Tokyo"' >> /usr/local/etc/php/conf.d/timezone.ini \
