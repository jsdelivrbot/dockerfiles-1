FROM jordiprats/centos5:5.11  
MAINTAINER KYBERNA AG <info@kyberna.com>  
  
COPY assets/init.sh /init.sh  
COPY assets/utterramblings.repo /etc/yum.repos.d/utterramblings.repo  
  
RUN rpm --import http://yum.jasonlitka.com/RPM-GPG-KEY-jlitka && \  
yum install -y epel-release && \  
yum upgrade -y && \  
yum install -y httpd mod_ssl openssl vixie-cron syslog \  
php php-apc php-cli php-common php-gd php-mbstring \  
php-mcrypt php-mhash php-mysql php-odbc php-pdo \  
php-pear php-pear-DB php-soap php-xml php-xmlrpc \  
php-bcmath php-imap \  
ImageMagick \  
postfix && \  
yum clean all && \  
mkdir /etc/httpd/vhost.d && \  
echo "Include vhost.d/*.conf" >> /etc/httpd/conf/httpd.conf && \  
chmod +x /init.sh  
  
WORKDIR /var/www/html  
  
EXPOSE 80 443  
  
CMD ["/init.sh"]  

