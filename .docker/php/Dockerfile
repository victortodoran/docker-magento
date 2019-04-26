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

RUN docker-php-ext-configure \
  gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

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

RUN apt-get install -y git

RUN curl -sS https://getcomposer.org/installer | \
  php -- --install-dir=/usr/local/bin --filename=composer --prefer-dist

# Install Xdebug
RUN pecl install xdebug && \
docker-php-ext-enable xdebug

# Install Mysql Client
RUN apt-get -y install mysql-client

# Node requires gnupg
RUN apt-get update && apt-get install -my wget gnupg

# Install NodeJS
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
  && apt-get install -yq nodejs build-essential

# Install common full-stack JavaScript packages globally
# http://blog.nodejs.org/2011/03/23/npm-1-0-global-vs-local-installation
RUN npm install -g yo grunt-cli

# Install gulp global
RUN npm install --global gulp

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

CMD ["/usr/local/bin/start"]
