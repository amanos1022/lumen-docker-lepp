FROM php:7.2.12-fpm-alpine

RUN set -ex \
	&& apk --no-cache add postgresql-libs postgresql-dev $PHPIZE_DEPS  git zip \
	&& docker-php-ext-install pgsql pdo_pgsql \
    && docker-php-ext-install -j$(nproc) iconv pdo pdo_mysql pdo_pgsql pgsql mbstring\
    && yes | pecl install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=on" >> /usr/local/etc/php/conf.d/xdebug.ini\
    && curl --silent --show-error https://getcomposer.org/installer | php\
    && mv composer.phar /usr/local/bin/composer;