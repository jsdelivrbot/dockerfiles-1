FROM ubuntu:14.04  
MAINTAINER Luis Elizondo "lelizondo@gmail.com"  
ENV DEBIAN_FRONTEND noninteractive  
  
# Ensure UTF-8  
RUN locale-gen en_US.UTF-8  
ENV LANG en_US.UTF-8  
ENV LC_ALL en_US.UTF-8  
# Prevent restarts when installing  
RUN echo '#!/bin/sh\nexit 101' > /usr/sbin/policy-rc.d && chmod +x
/usr/sbin/policy-rc.d  
  
# Update System & Basic packages  
RUN apt-get update \  
&& apt-get dist-upgrade -y \  
&& apt-get -y install php5-fpm \  
php5-mysql \  
php-apc php5-imagick \  
php5-imap \  
php5-mcrypt \  
php5-curl \  
php5-cli \  
php5-gd \  
php5-pgsql \  
php5-sqlite \  
php5-common \  
php-pear curl \  
php5-json \  
php5-redis \  
php5-memcache \  
nginx-extras \  
git \  
supervisor \  
ca-certificates \  
openssl \  
sendmail --no-install-recommends \  
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  
  
RUN php5enmod mcrypt  
  
RUN /usr/bin/curl -sS https://getcomposer.org/installer | /usr/bin/php  
RUN /bin/mv composer.phar /usr/local/bin/composer  
  
# Install Composer and Drush 6.7  
RUN /usr/bin/curl -sS https://getcomposer.org/installer | /usr/bin/php  
RUN /bin/mv composer.phar /usr/local/bin/composer  
RUN /usr/local/bin/composer self-update  
RUN mkdir --parents /opt/drush-6.7 && cd /opt/drush-6.7 && composer init
--require=drush/drush:6.* -n && /usr/local/bin/composer config bin-dir
/usr/local/bin && /usr/local/bin/composer install  
  
# Prepare directory  
RUN mkdir /var/www  
RUN usermod -u 1000 www-data  
RUN usermod -a -G users www-data  
RUN chown -R www-data:www-data /var/www  
  
WORKDIR /var/www  
  
# Startup script  
# This startup script wll configure nginx  
ADD ./startup.sh /opt/startup.sh  
RUN chmod +x /opt/startup.sh  
  
RUN mkdir -p /var/cache/nginx/microcache  
  
# Avoid sendmail starting as a service  
RUN update-rc.d sendmail disable  
  
### Add configuration files  
# Supervisor  
ADD ./config/supervisor/supervisord-nginx.conf
/etc/supervisor/conf.d/supervisord-nginx.conf  
  
# PHP  
ADD ./config/php/www.conf /etc/php5/fpm/pool.d/www.conf  
ADD ./config/php/php.ini /etc/php5/fpm/php.ini  
  
# Nginx  
ADD ./config/nginx/blacklist.conf /etc/nginx/blacklist.conf  
ADD ./config/nginx/drupal.conf /etc/nginx/drupal.conf  
ADD ./config/nginx/drupal_upload_progress.conf
/etc/nginx/drupal_upload_progress.conf  
ADD ./config/nginx/fastcgi.conf /etc/nginx/fastcgi.conf  
ADD ./config/nginx/fastcgi_drupal.conf /etc/nginx/fastcgi_drupal.conf  
ADD ./config/nginx/fastcgi_microcache_zone.conf
/etc/nginx/fastcgi_microcache_zone.conf  
ADD ./config/nginx/fastcgi_no_args_drupal.conf
/etc/nginx/fastcgi_no_args_drupal.conf  
ADD ./config/nginx/map_cache.conf /etc/nginx/map_cache.conf  
ADD ./config/nginx/microcache_fcgi.conf /etc/nginx/microcache_fcgi.conf  
ADD ./config/nginx/microcache_fcgi_auth.conf
/etc/nginx/microcache_fcgi_auth.conf  
ADD ./config/nginx/mime.types /etc/nginx/mime.types  
ADD ./config/nginx/nginx.conf /etc/nginx/nginx.conf  
ADD ./config/nginx/upstream_phpcgi_unix.conf
/etc/nginx/upstream_phpcgi_unix.conf  
ADD ./config/nginx/map_block_http_methods.conf
/etc/nginx/map_block_http_methods.conf  
ADD ./config/nginx/map_https_fcgi.conf /etc/nginx/map_https_fcgi.conf  
ADD ./config/nginx/nginx_status_allowed_hosts.conf
/etc/nginx/nginx_status_allowed_hosts.conf  
ADD ./config/nginx/cron_allowed_hosts.conf /etc/nginx/cron_allowed_hosts.conf  
ADD ./config/nginx/php_fpm_status_allowed_hosts.conf
/etc/nginx/php_fpm_status_allowed_hosts.conf  
ADD ./config/nginx/default /etc/nginx/sites-enabled/default  
  
# Private expose  
EXPOSE 80  
# Run startup script  
CMD ["/bin/bash", "/opt/startup.sh"]  

