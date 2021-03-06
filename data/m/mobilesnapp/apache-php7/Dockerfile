############################################  
# Dockerfile to build Jenkins service image  
############################################  
# Base image  
FROM debian:jessie  
  
# Author: MobileSnapp Inc.  
MAINTAINER MobileSnapp <support@mobilesnapp.com>  
  
# persistent / runtime deps  
ENV PHPIZE_DEPS \  
autoconf \  
file \  
g++ \  
gcc \  
libc-dev \  
make \  
pkg-config \  
re2c  
RUN apt-get update && apt-get install -y \  
$PHPIZE_DEPS \  
ca-certificates \  
curl \  
libedit2 \  
libsqlite3-0 \  
libxml2 \  
\--no-install-recommends && rm -r /var/lib/apt/lists/*  
  
ENV PHP_INI_DIR /usr/local/etc/php  
RUN mkdir -p $PHP_INI_DIR/conf.d  
  
# Install apache.  
RUN apt-get update && apt-get install -y apache2-bin apache2.2-common --no-
install-recommends && rm -rf /var/lib/apt/lists/*  
  
RUN rm -rf /var/www/html && mkdir -p /var/lock/apache2 /var/run/apache2
/var/log/apache2 /var/www/html && chown -R www-data:www-data /var/lock/apache2
/var/run/apache2 /var/log/apache2 /var/www/html  
  
# Apache + PHP requires preforking Apache for best results  
RUN a2dismod mpm_event && a2enmod mpm_prefork  
  
RUN mv /etc/apache2/apache2.conf /etc/apache2/apache2.conf.dist && rm
/etc/apache2/conf-enabled/* /etc/apache2/sites-enabled/*  
COPY apache2.conf /etc/apache2/apache2.conf  
# COPY apache2.conf as its contents are checked by PHP during compilation  
ENV PHP_EXTRA_BUILD_DEPS apache2-dev  
ENV PHP_EXTRA_CONFIGURE_ARGS --with-apxs2  
  
ENV GPG_KEYS 1A4E8B7277C42E53DBA9C7B9BCAA30EA9C0D5763  
  
ENV PHP_VERSION 7.0.7  
ENV PHP_FILENAME php-7.0.7.tar.xz  
ENV PHP_SHA256
9cc64a7459242c79c10e79d74feaf5bae3541f604966ceb600c3d2e8f5fe4794  
  
RUN set -xe \  
&& buildDeps=" \  
$PHP_EXTRA_BUILD_DEPS \  
libcurl4-openssl-dev \  
libedit-dev \  
libsqlite3-dev \  
libssl-dev \  
libxml2-dev \  
xz-utils \  
" \  
&& apt-get update && apt-get install -y $buildDeps \--no-install-recommends &&
rm -rf /var/lib/apt/lists/* \  
&& curl -fSL "http://php.net/get/$PHP_FILENAME/from/this/mirror" -o
"$PHP_FILENAME" \  
&& echo "$PHP_SHA256 *$PHP_FILENAME" | sha256sum -c - \  
&& curl -fSL "http://php.net/get/$PHP_FILENAME.asc/from/this/mirror" -o
"$PHP_FILENAME.asc" \  
&& export GNUPGHOME="$(mktemp -d)" \  
&& for key in $GPG_KEYS; do \  
gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \  
done \  
&& gpg --batch --verify "$PHP_FILENAME.asc" "$PHP_FILENAME" \  
&& rm -r "$GNUPGHOME" "$PHP_FILENAME.asc" \  
&& mkdir -p /usr/src/php \  
&& tar -xf "$PHP_FILENAME" -C /usr/src/php --strip-components=1 \  
&& rm "$PHP_FILENAME" \  
&& cd /usr/src/php \  
&& ./configure \  
\--with-config-file-path="$PHP_INI_DIR" \  
\--with-config-file-scan-dir="$PHP_INI_DIR/conf.d" \  
$PHP_EXTRA_CONFIGURE_ARGS \  
\--disable-cgi \  
# --enable-mysqlnd is included here because it's harder to compile after the
fact than extensions are (since it's a plugin for several extensions, not an
extension in itself)  
\--enable-mysqlnd \  
# --enable-mbstring is included here because otherwise there's no way to get
pecl to use it properly (see https://github.com/docker-library/php/issues/195)  
\--enable-mbstring \  
\--with-curl \  
\--with-libedit \  
\--with-openssl \  
\--with-zlib \  
&& make -j"$(nproc)" \  
&& make install \  
&& { find /usr/local/bin /usr/local/sbin -type f -executable -exec strip
--strip-all '{}' \+ || true; } \  
&& make clean \  
&& apt-get purge -y --auto-remove -o
APT::AutoRemove::RecommendsImportant=false -o
APT::AutoRemove::SuggestsImportant=false $buildDeps  
  
COPY docker-php-ext-* /usr/local/bin/  
  
RUN /usr/sbin/a2dismod 'mpm_*' && /usr/sbin/a2enmod mpm_prefork  
  
COPY apache2-foreground /usr/local/bin/  
COPY index.php /var/www/html  
WORKDIR /var/www/html  
  
# Manually set up the apache environment variables  
ENV APACHE_RUN_USER www-data  
ENV APACHE_RUN_GROUP www-data  
ENV APACHE_LOG_DIR /var/log/apache2  
ENV APACHE_LOCK_DIR /var/lock/apache2  
ENV APACHE_PID_FILE /var/run/apache2.pid  
  
# Expose web port  
EXPOSE 80  
# Expose SSL port  
EXPOSE 443  
# Update the default apache site with the config we created.  
ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf  
  
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

