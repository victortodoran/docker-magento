FROM php:7.1-fpm

RUN apt-get update \
  && apt-get install -y \
    cron \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    mysql-client \
    libxslt1-dev

RUN docker-php-ext-configure gd \
    --enable-gd-native-ttf --with-freetype-dir=/usr/include/freetype2 --with-png-dir=/usr/include --with-jpeg-dir=/usr/include

RUN docker-php-ext-install \
  bcmath \
  gd \
  intl \
  mbstring \
  mcrypt \
  pdo_mysql \
  soap \
  xsl \
  zip

RUN apt-get install -y git libmemcached-dev libmemcached11

#Adding memcached library, fittable with/for PHP7
RUN git clone -b php7 https://github.com/php-memcached-dev/php-memcached /usr/src/php/ext/memcached \
 && docker-php-ext-configure /usr/src/php/ext/memcached \
     --disable-memcached-sasl \
 && docker-php-ext-install /usr/src/php/ext/memcached \
 && rm -rf /usr/src/php/ext/memcached


RUN curl -sS https://getcomposer.org/installer | \
  php -- --install-dir=/usr/local/bin --filename=composer --prefer-dist

# Install Xdebug
RUN pecl install xdebug && \
docker-php-ext-enable xdebug

# Install Mysql Client
RUN apt-get -y install mysql-client

# Install Mailcatcher
RUN apt-get update

RUN apt-get -y install build-essential ruby-full libsqlite3-dev &&\
    gem install mailcatcher --no-rdoc --no-ri

# Install nano
RUN apt-get install -y nano

ENV PHP_MEMORY_LIMIT 2G
ENV PHP_PORT 9000
ENV PHP_PM dynamic
ENV PHP_PM_MAX_CHILDREN 10
ENV PHP_PM_START_SERVERS 4
ENV PHP_PM_MIN_SPARE_SERVERS 2
ENV PHP_PM_MAX_SPARE_SERVERS 6
ENV APP_MAGE_MODE default

COPY conf/www.conf /usr/local/etc/php-fpm.d/
COPY conf/php.ini /usr/local/etc/php/
COPY conf/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
COPY conf/php-fpm.conf /usr/local/etc/
COPY bin/* /usr/local/bin/

RUN usermod -u 1000 www-data
RUN usermod -G 100 www-data

WORKDIR /var/www/html
EXPOSE 9000

CMD ["/usr/local/bin/start"]
