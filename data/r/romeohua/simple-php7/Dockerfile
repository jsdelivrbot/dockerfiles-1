FROM centos:7  
MAINTAINER Romeo Hua <romeohua@hotmail.com>  
##  
# Nginx: 1.10.0  
# PHP : 7.0.6  
##  
#Install system library  
#RUN yum update -y  
ENV NGINX_VERSION 1.10.0  
ENV PHP_VERSION 7.0.6  
RUN yum install -y gcc \  
gcc-c++ \  
autoconf \  
automake \  
libtool \  
make \  
cmake && \  
yum clean all  
  
#Install PHP library  
## libmcrypt-devel DIY  
RUN rpm -ivh http://dl.fedoraproject.org/pub/epel/6/i386/epel-
release-6-8.noarch.rpm && \  
yum install -y wget \  
zlib \  
zlib-devel \  
openssl \  
openssl-devel \  
pcre-devel \  
libxml2 \  
libxml2-devel \  
libcurl \  
libcurl-devel \  
libpng-devel \  
libjpeg-devel \  
freetype-devel \  
libmcrypt-devel \  
openssh-server \  
python-setuptools && \  
yum clean all  
  
#Add user  
RUN groupadd -r www && \  
useradd -M -s /sbin/nologin -r -g www www  
  
#Download nginx & php  
RUN mkdir -p /home/nginx-php && cd $_ && \  
wget -c -O nginx.tar.gz http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz
&& \  
wget -O php.tar.gz http://php.net/distributions/php-$PHP_VERSION.tar.gz  
  
#Make install nginx  
RUN cd /home/nginx-php && \  
tar -zxvf nginx.tar.gz && \  
cd nginx-$NGINX_VERSION && \  
./configure --prefix=/usr/local/nginx \  
\--user=www --group=www \  
\--error-log-path=/var/log/nginx_error.log \  
\--http-log-path=/var/log/nginx_access.log \  
\--pid-path=/var/run/nginx.pid \  
\--with-pcre \  
\--with-http_ssl_module \  
\--without-mail_pop3_module \  
\--without-mail_imap_module \  
\--with-http_gzip_static_module && \  
make && make install  
  
#Make install php  
RUN cd /home/nginx-php && \  
tar zvxf php.tar.gz && \  
cd php-$PHP_VERSION && \  
./configure --prefix=/usr/local/php \  
\--with-config-file-path=/usr/local/php/etc \  
\--with-config-file-scan-dir=/usr/local/php/etc/php.d \  
\--with-fpm-user=www \  
\--with-fpm-group=www \  
\--with-mcrypt=/usr/include \  
\--with-mysqli \  
\--with-pdo-mysql \  
\--with-openssl \  
\--with-gd \  
\--with-iconv \  
\--with-zlib \  
\--with-gettext \  
\--with-curl \  
\--with-png-dir \  
\--with-jpeg-dir \  
\--with-freetype-dir \  
\--with-xmlrpc \  
\--with-mhash \  
\--enable-fpm \  
\--enable-xml \  
\--enable-shmop \  
\--enable-sysvsem \  
\--enable-inline-optimization \  
\--enable-mbregex \  
\--enable-mbstring \  
\--enable-ftp \  
\--enable-gd-native-ttf \  
\--enable-mysqlnd \  
\--enable-pcntl \  
\--enable-sockets \  
\--enable-zip \  
\--enable-soap \  
\--enable-session \  
\--enable-opcache \  
\--enable-bcmath \  
\--enable-exif \  
\--enable-fileinfo \  
\--disable-rpath \  
\--enable-ipv6 \  
\--disable-debug \  
\--without-pear && \  
make && make install  
  
RUN cd /home/nginx-php/php-$PHP_VERSION && \  
cp php.ini-production /usr/local/php/etc/php.ini && \  
cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf  
  
ADD www.conf /usr/local/php/etc/php-fpm.d/www.conf  
  
#Install supervisor  
RUN easy_install supervisor && \  
mkdir -p /var/log/supervisor && \  
mkdir -p /var/run/sshd && \  
mkdir -p /var/run/supervisord  
  
#Add supervisord conf  
ADD supervisord.conf /etc/supervisord.conf  
  
#Remove zips  
RUN cd / && rm -rf /home/nginx-php  
  
#Create web folder  
VOLUME ["/data/www", "/usr/local/nginx/conf/ssl",
"/usr/local/nginx/conf/vhost", "/usr/local/php/etc/php.d"]  
  
RUN mkdir -p /data/www/public  
  
ADD index.php /data/www/public/index.php  
  
#Update nginx config  
ADD nginx.conf /usr/local/nginx/conf/nginx.conf  
  
#Start  
ADD start.sh /start.sh  
RUN chmod +x /start.sh  
  
#Set port  
EXPOSE 80 443 9001  
#Start it  
ENTRYPOINT ["/start.sh"]  
  
#Start web server  
#CMD ["/bin/bash", "/start.sh"]  

