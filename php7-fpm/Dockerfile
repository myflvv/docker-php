FROM daocloud.io/library/php:7.2.7-fpm
COPY ./sources.list /etc/apt/sources.list
RUN apt-get update && apt-get install -y --no-install-recommends \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libc-client-dev \
    libkrb5-dev \
    zip \
    unzip \
    git \
    screen \
    #swoole 依赖扩展
    libpcre2-dev \
    libhiredis-dev \
    #debian9的git版本是2.17,swoftcli需要使用git的"on-tags"参数，需要编译安装git，需要以下依赖库
    make \
    libssl-dev \
    libghc-zlib-dev \
    libcurl4-gnutls-dev \
    libexpat1-dev \
    gettext \
    #git install
    && curl -OL https://github.com/git/git/archive/v2.23.0.zip \
    && unzip v2.23.0.zip \
    && cd git-2.23.0 \
    && make prefix=/usr/local all \
    && make prefix=/usr/local install \
    #swoftcli install
    && curl -OL https://github.com/swoft-cloud/swoft-cli/releases/download/v0.1.3/swoftcli.phar \
    && mv swoftcli.phar /usr/bin/swoftcli \
    && chmod +x /usr/bin/swoftcli \
    ######
    && docker-php-ext-install iconv  \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd pdo pdo_mysql zip bcmath \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install -j$(nproc) imap \
    #composer install
    && php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://packagist.phpcomposer.com \
    #pecl install
    && pecl install redis \
    && docker-php-ext-enable redis \ 
    && pecl install swoole \
    && docker-php-ext-enable swoole \
    #删除无用的安装包
    && rm -r /var/lib/apt/lists/* 
# RUN mkdir -p /usr/src/php/ext/redis \
#	&& curl -L https://github.com/phpredis/phpredis/archive/4.1.0.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
#	&& echo 'redis' >> /usr/src/php-available-exts \
#	&& docker-php-ext-install redis
# CMD ["php-fpm"]