FROM daocloud.io/library/php:7.1.20-fpm
ADD sources.list /etc/apt/sources.list
######
# You can install php extensions using docker-php-ext-install
######

#RUN apt-get update && apt-get install -y \
#        libfreetype6-dev \
#        libjpeg62-turbo-dev \
#        libmcrypt-dev \
#        libpng12-dev \
#    && docker-php-ext-install -j$(nproc) iconv  \
#    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
#    && docker-php-ext-install -j$(nproc) gd pdo pdo_mysql

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        screen \
        #swoole 
        libpcre2-dev \
        libhiredis-dev \
        # libpng12-dev
	&& docker-php-ext-install -j$(nproc) iconv mcrypt bcmath \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
	&& docker-php-ext-install -j$(nproc)  mysqli  zip mbstring pdo_mysql

RUN curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/4.1.0.tar.gz \
    && tar xfz /tmp/redis.tar.gz \
    && rm -r /tmp/redis.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv phpredis-4.1.0 /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
    && rm -rf /usr/src/php \
    # swoole
    && curl 'http://pecl.php.net/get/swoole-4.2.1.tgz' -o swoole-4.2.1.tgz \
    && pecl install swoole-4.2.1.tgz \
    && rm -rf /var/www/html/swoole-4.2.1.tgz \
    && docker-php-ext-enable swoole

#RUN pecl install swoole