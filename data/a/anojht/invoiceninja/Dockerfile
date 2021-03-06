FROM php:7.2-fpm  
  
MAINTAINER Anojh Thayaparan <athayapa@sfu.ca>  
  
#####  
# SYSTEM REQUIREMENT  
#####  
ENV PHANTOMJS phantomjs-2.1.1-linux-x86_64  
RUN apt-get update \  
&& apt-get install -y --no-install-recommends \  
zlib1g-dev git libgmp-dev unzip \  
libfreetype6-dev libjpeg62-turbo-dev libpng-dev \  
build-essential chrpath libssl-dev libxft-dev \  
libfreetype6 libfontconfig1 libfontconfig1-dev \  
nginx nano \  
&& ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/ \  
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-
dir=/usr/include/ \  
&& docker-php-ext-configure gmp \  
&& docker-php-ext-install iconv mbstring pdo pdo_mysql zip gd gmp opcache \  
&& curl -o ${PHANTOMJS}.tar.bz2 -SL
https://bitbucket.org/ariya/phantomjs/downloads/${PHANTOMJS}.tar.bz2 \  
&& tar xvjf ${PHANTOMJS}.tar.bz2 \  
&& rm ${PHANTOMJS}.tar.bz2 \  
&& mv ${PHANTOMJS} /usr/local/share \  
&& ln -sf /usr/local/share/${PHANTOMJS}/bin/phantomjs /usr/local/bin \  
&& rm -rf /var/lib/apt/lists/*  
  
# set recommended PHP.ini settings  
# see https://secure.php.net/manual/en/opcache.installation.php  
RUN { \  
echo 'opcache.memory_consumption=128'; \  
echo 'opcache.interned_strings_buffer=8'; \  
echo 'opcache.max_accelerated_files=4000'; \  
echo 'opcache.revalidate_freq=60'; \  
echo 'opcache.fast_shutdown=1'; \  
echo 'opcache.enable_cli=1'; \  
} > /usr/local/etc/php/conf.d/opcache-recommended.ini  
  
#####  
# DOWNLOAD AND INSTALL INVOICE NINJA  
#####  
ENV INVOICENINJA_VERSION 4.4.3  
RUN curl -o ninja.zip -SL
https://download.invoiceninja.com/ninja-v${INVOICENINJA_VERSION}.zip \  
&& ls . \  
&& unzip ninja.zip -d /var/www/ \  
&& rm ninja.zip \  
&& mv /var/www/ninja /var/www/app \  
&& mv /var/www/app/storage /var/www/app/docker-backup-storage \  
&& mv /var/www/app/public /var/www/app/docker-backup-public \  
&& mkdir -p /var/www/app/public/logo /var/www/app/storage \  
&& touch /var/www/app/.env \  
&& chmod -R 755 /var/www/app/storage \  
&& chown -R www-data:www-data /var/www/app/storage /var/www/app/bootstrap
/var/www/app/public/logo /var/www/app/.env /var/www/app/docker-backup-storage
/var/www/app/docker-backup-public \  
&& rm -rf /var/www/app/docs /var/www/app/tests /var/www/ninja  
  
######  
# DEFAULT ENV  
######  
ENV LOG errorlog  
ENV SELF_UPDATER_SOURCE ''  
ENV PHANTOMJS_BIN_PATH /usr/local/bin/phantomjs  
  
  
#use to be mounted into nginx for exemple  
VOLUME /var/www/app/public  
  
WORKDIR /var/www/app  
  
COPY docker-compose/nginx.conf /etc/nginx/nginx.conf  
EXPOSE 80  
COPY docker-compose/cronscript.sh /cronscript.sh  
COPY entrypoint.sh /entrypoint.sh  
RUN chmod +x /entrypoint.sh /cronscript.sh  
  
ENTRYPOINT ["/entrypoint.sh"]  
CMD ["php-fpm"]  

