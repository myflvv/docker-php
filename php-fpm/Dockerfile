FROM daocloud.io/library/php:7.1.20-fpm
ADD sources.list /etc/apt/sources.list
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        screen \
        #swoole 
        #libpcre2-dev \
        #libhiredis-dev \
        # libpng12-dev
	&& docker-php-ext-install -j$(nproc) iconv mcrypt bcmath gd mysqli  zip mbstring pdo_mysql sockets\
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ 

#pecl install
RUN pecl install redis \
    && docker-php-ext-enable redis 
    #&& pecl install swoole \
    #&& docker-php-ext-enable swoole

# php composer
#RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \
    #&& php composer-setup.php \
    #&& php -r "unlink('composer-setup.php');" \
    #&& mv composer.phar /usr/local/bin/composer \
    #&& composer config -g repo.packagist composer https://packagist.phpcomposer.com

COPY composer.phar /usr/local/bin/composer

#下载安装
#RUN curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/4.1.0.tar.gz \
#    && tar xfz /tmp/redis.tar.gz \
#    && rm -r /tmp/redis.tar.gz \
#    && mkdir -p /usr/src/php/ext \
#    && mv phpredis-4.1.0 /usr/src/php/ext/redis \
#    && docker-php-ext-install redis \
#    && rm -rf /usr/src/php \
#    # swoole
#    && curl 'http://pecl.php.net/get/swoole-4.3.3.tgz' -o swoole-4.3.3.tgz \
#    && pecl install swoole-4.3.3.tgz \
#    && rm -rf /var/www/html/swoole-4.3.3.tgz \
#    && docker-php-ext-enable swoole 