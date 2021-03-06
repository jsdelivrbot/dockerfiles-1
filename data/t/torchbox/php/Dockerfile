FROM php:7-fpm  
  
MAINTAINER Torchbox Sysadmin <sysadmin@torchbox.com>  
  
ENV DEBIAN_FRONTEND noninteractive  
  
RUN apt-get update && apt-get install -y \  
git \  
mysql-client \  
libfreetype6-dev \  
libjpeg62-turbo-dev \  
libmcrypt-dev \  
libpng12-dev \  
libssl-dev \  
libmemcached-dev \  
libz-dev \  
libmysqlclient18 \  
zlib1g-dev \  
libsqlite3-dev \  
zip \  
libxml2-dev \  
libcurl3-dev \  
libedit-dev \  
libpspell-dev \  
libldap2-dev \  
unixodbc-dev \  
libpq-dev  
  
# https://bugs.php.net/bug.php?id=49876  
RUN ln -fs /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/  
  
RUN echo "Installing PHP extensions" \  
&& docker-php-ext-install -j$(nproc) iconv mcrypt gd pdo_mysql pdo_pgsql pcntl
pdo_sqlite zip curl bcmath opcache simplexml xmlrpc xml soap session readline
pspell ldap mbstring \  
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-
dir=/usr/include/ \  
&& docker-php-ext-enable iconv mcrypt gd pdo_mysql pdo_pgsql pcntl pdo_sqlite
zip curl bcmath opcache simplexml xmlrpc xml soap session readline pspell ldap
mbstring \  
&& git clone -b php7 https://github.com/php-memcached-dev/php-memcached.git
/usr/src/php/ext/memcached \  
&& cd /usr/src/php/ext/memcached \  
&& git checkout origin/php7 \  
&& docker-php-ext-configure memcached \  
&& docker-php-ext-install memcached \  
&& apt-get autoremove -y \  
&& dpkg -la | awk '{print $2}' | grep '\-dev' | xargs apt-get remove -y \  
&& apt-get clean all \  
&& rm -rvf /var/lib/apt/lists/* \  
&& rm -rvf /usr/share/doc /usr/share/man /usr/share/locale \  
&& rm -fv /usr/local/etc/php-fpm.d/*.conf \  
&& rm -rvf /usr/src/php  
  
# install composer  
RUN curl -sS https://getcomposer.org/installer | php -- --filename=composer
--install-dir=/bin  
ENV PATH /root/.composer/vendor/bin:$PATH  
  
# install phpunit  
RUN curl https://phar.phpunit.de/phpunit.phar -L > phpunit.phar \  
&& chmod +x phpunit.phar \  
&& mv phpunit.phar /usr/local/bin/phpunit \  
&& phpunit --version  
  
EXPOSE 9000  

