######
# See: https://hub.docker.com/_/php/
######

FROM daocloud.io/library/php:5.6.36-fpm
MAINTAINER micooz <micooz@hotmail.com>
ADD sources.list /etc/apt/sources.list
######
# You can install php extensions using docker-php-ext-install
######
#RUN mkdir -p /usr/share/nginx/php56html
#RUN apt-get update && apt-get install -y \
#        libfreetype6-dev \
#        libjpeg62-turbo-dev \
#        libmcrypt-dev \
#        libpng12-dev \
#    && docker-php-ext-install -j$(nproc) iconv mcrypt \
#    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
#    && docker-php-ext-install -j$(nproc) gd

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev
        # libpng12-dev
RUN docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd 

RUN docker-php-ext-install -j$(nproc)  mysqli  zip mbstring pdo_mysql