FROM teodorescuserban/kobo-base-mongo:latest  
  
MAINTAINER Serban Teodorescu, teodorescu.serban@gmail.com  
  
COPY run_mongo /etc/service/mongo/run  
COPY add_index.sh /srv/  
  
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh && \  
chmod +x /etc/service/mongo/run && \  
mkdir -p /srv/db  
  
VOLUME ["/srv/db"]  
  
EXPOSE 27017  
CMD ["/sbin/my_init"]  

