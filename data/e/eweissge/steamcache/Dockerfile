FROM alpine:latest  
MAINTAINER SteamCache.Net Team <team@steamcache.net>  
  
ENV STEAMCACHE_VERSION 6  
ENV WEBUSER nginx  
  
RUN apk update \  
&& apk add \  
openssl \  
nginx  
  
COPY overlay/ /  
  
RUN chmod 755 /scripts/* ;\  
mkdir -m 755 -p /data/cache ;\  
mkdir -m 755 -p /data/info ;\  
mkdir -m 755 -p /data/logs ;\  
mkdir -m 755 -p /tmp/nginx/ ;\  
chown -R ${WEBUSER}:${WEBUSER} /data/ ;\  
mkdir -p /etc/nginx/sites-enabled ;\  
ln -s /etc/nginx/sites-available/steamcache.conf /etc/nginx/sites-
enabled/steamcache.conf  
  
#ADD games.tar.gz /data/cache  
#VOLUME ["/data/logs", "/data/cache", "/var/www"]  
EXPOSE 80  
WORKDIR /scripts  
  
ENV LANCACHE_IP 192.168.1.3  
ENV STEAMCACHE_IP 192.168.1.3  
ENV UPLAYCACHE_IP 192.168.1.3  
ENV WINDOWSCACHE_IP 192.168.1.3  
ENTRYPOINT ["/scripts/bootstrap.sh"]  

