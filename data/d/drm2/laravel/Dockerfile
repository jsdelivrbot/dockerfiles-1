FROM laradock/php-fpm:1.4-71  
MAINTAINER David R. Myers II <davidrmyersii@gmail.com>  
RUN apt-get update && \  
apt-get install -y git zip unzip && \  
rm -rf /var/lib/apt/lists/* && \  
docker-php-ext-install zip && \  
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \  
php -r "if (hash_file('SHA384', 'composer-setup.php') ===
'669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410')
{ echo 'Installer verified'; } else { echo 'Installer corrupt';
unlink('composer-setup.php'); } echo PHP_EOL;" && \  
php composer-setup.php && \  
php -r "unlink('composer-setup.php');" && \  
mv composer.phar /usr/local/bin/composer  
RUN usermod -u 1000 www-data  
WORKDIR /var/www  
EXPOSE 9000  
CMD ["php-fpm"]  

