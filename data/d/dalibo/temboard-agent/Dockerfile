FROM python:3.6-slim  
  
RUN apt-get update -y \  
&& mkdir -p /usr/share/man/man1 /usr/share/man/man7 \  
&& apt-get install -y --no-install-recommends \  
libltdl7 \  
postgresql-client \  
sudo \  
git-core \  
&& apt-get clean \  
&& rm -rf /var/lib/apt/lists/* \  
;  
  
ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-
it.sh /usr/local/bin/wait-for-it  
  
RUN chmod 0755 /usr/local/bin/wait-for-it \  
&& groupadd --system docker \  
&& useradd --home-dir /var/lib/postgresql \--create-home --system --groups
docker postgres  
  
VOLUME /var/lib/temboard-agent  
WORKDIR /var/lib/temboard-agent  
VOLUME /etc/temboard-agent  
ENTRYPOINT ["docker-entrypoint.sh"]  
CMD ["temboard-agent"]  
  
ADD sudoers /etc/sudoers.d/temboard-agent  
ADD entrypoint.sh /usr/local/bin/docker-entrypoint.sh  
RUN git clone --depth=1 \--recursive https://github.com/dalibo/temboard-agent
/tmp/temboard-agent && \  
pip install --no-cache-dir /tmp/temboard-agent && \  
rm -rf /tmp/temboard-agent  

