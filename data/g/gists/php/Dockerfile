FROM alpine:3.7  
MAINTAINER UmVnaXN0ZXIgcmVnaXN0ZXJkZWRpY2F0ZWQrZG9ja2VyKGF0KWdtYWlsLmNvbQo=  
  
# Environments  
ENV MEMORY_LIMIT 256M  
ENV UPLOAD_MAX_FILESIZE 64M  
ENV MAX_FILE_UPLOADS 20  
ENV POST_MAX_SIZE 64M  
ENV MAX_INPUT_VARS 4000  
ENV DATE_TIMEZONE Asia/Shanghai  
ENV PM_MAX_CHILDREN 6  
ENV PM_START_SERVERS 4  
ENV PM_MIN_SPARE_SERVERS 2  
ENV PM_MAX_SPARE_SERVERS 6  
ENV UID 100  
ENV GID 101  
# Let's roll  
RUN set -xe && \  
apk add --no-cache \  
php7-mbstring \  
php7-mcrypt \  
php7-soap \  
php7-opcache \  
php7-openssl \  
php7-gmp \  
php7-json \  
php7-dom \  
php7-zip \  
php7-mysqli \  
php7-mysqlnd \  
php7-sqlite3 \  
php7-bcmath \  
php7-gd \  
php7-odbc \  
php7-pdo \  
php7-pdo_mysql \  
php7-pdo_sqlite \  
php7-pdo_odbc \  
php7-pdo_pgsql \  
php7-pdo_dblib \  
php7-gettext \  
php7-xmlreader \  
php7-xmlrpc \  
php7-bz2 \  
php7-iconv \  
php7-curl \  
php7-ctype \  
php7-fpm  
  
COPY entrypoint.sh /usr/bin/entrypoint.sh  
  
WORKDIR /var/www  
  
VOLUME ["/var/www"]  
  
ENTRYPOINT ["/usr/bin/entrypoint.sh"]  
  
CMD ["/usr/sbin/php-fpm7"]  

