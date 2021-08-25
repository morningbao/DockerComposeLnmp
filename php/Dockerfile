FROM php:7.3.29-fpm

# Version
ENV PHPREDIS_VERSION 4.0.1

# Timezone
RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo 'Asia/Shanghai' > /etc/timezone \
# 安装依赖
&& apt-get update \
&& apt-get install -y procps vim curl wget git zip libz-dev libssl-dev libnghttp2-dev libpcre3-dev libpng-dev libxml2-dev libzip-dev \
&& apt-get -y clean \
&& apt-get -y autoremove \
# 安装扩展
&& docker-php-ext-install bcmath gd gettext pcntl pdo_mysql shmop soap sockets sysvsem xmlrpc zip \
&& echo zend_extension=opcache.so > /usr/local/etc/php/conf.d/zend_extension.ini \
# 安装composer
&&  curl -sS https://getcomposer.org/installer | php \
&& mv composer.phar /usr/local/bin/composer \
&& composer self-update --clean-backups \
# 源码安装目录
&& mkdir /opt/packet /opt/source \
# 安装redis
&& cd /opt/packet \
&& wget http://pecl.php.net/get/redis-${PHPREDIS_VERSION}.tgz -O ./redis.tar.tgz \
&& pecl install ./redis.tar.tgz \
&& docker-php-ext-enable redis \
# 安装nghttp2
&& cd /opt/packet/ \
&& wget https://github.com/nghttp2/nghttp2/releases/download/v1.34.0/nghttp2-1.34.0.tar.gz \
&& tar zxvf nghttp2-1.34.0.tar.gz -C ../source/ \
&& cd /opt/source/nghttp2-1.34.0/ \
&& ./configure && make && make install \
# 删除目录
&& rm -rf /opt/packet /opt/source && rm -rf /var/lib/apt/lists/*

WORKDIR /srv/http
