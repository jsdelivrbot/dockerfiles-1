FROM ubuntu:xenial  
  
RUN \  
apt-get update \  
&& apt-get install -y curl \  
&& echo deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main >
/etc/apt/sources.list.d/pgdg.list \  
&& curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add \- \  
&& apt-get update \  
&& apt-get install -y --no-install-recommends \  
cron \  
duplicity \  
lftp \  
postgresql-client \  
python-paramiko \  
openssh-client \  
&& rm -rf /var/lib/apt/lists/*  
  
COPY backup.sh /opt/  
COPY start.sh /opt/  
  
RUN chmod u+x /opt/*.sh  
  
VOLUME /backup  
  
CMD ["/opt/start.sh"]

