FROM mongo:3.0  
MAINTAINER Ilya Stepanov <dev@ilyastepanov.com>  
  
RUN apt-get update && \  
apt-get install -y cron python python-pip && \  
pip install awscli && \  
apt-get clean && rm -rf /var/lib/apt/lists/*  
  
ADD backup.sh /backup.sh  
RUN chmod +x /backup.sh  
  
ADD start.sh /start.sh  
RUN chmod +x /start.sh  
  
VOLUME /backup  
  
#ENTRYPOINT ["/start.sh"]  
CMD ["/start.sh"]  

