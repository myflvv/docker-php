FROM daocloud.io/library/php:7.2.7-fpm
COPY ./sources.list /etc/apt/sources.list
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
    && docker-php-ext-install iconv  \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd pdo pdo_mysql 
 RUN mkdir -p /usr/src/php/ext/redis \
	&& curl -L https://github.com/phpredis/phpredis/archive/4.1.0.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
	&& echo 'redis' >> /usr/src/php-available-exts \
	&& docker-php-ext-install redis
# CMD ["php-fpm"]