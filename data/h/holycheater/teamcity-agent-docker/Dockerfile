FROM ubuntu:14.04  
ENV AGENT_DIR /opt/buildAgent  
  
RUN apt-get update \  
&& apt-get install -y --no-install-recommends \  
lxc iptables aufs-tools ca-certificates curl wget software-properties-common
language-pack-en unzip \  
&& rm -rf /var/lib/apt/lists/*  
  
# Fix locale.  
ENV LANG en_US.UTF-8  
ENV LC_CTYPE en_US.UTF-8  
RUN locale-gen en_US && update-locale LANG=en_US.UTF-8 LC_CTYPE=en_US.UTF-8  
  
# grab gosu for easy step-down from root  
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys
B42F6819007F00F88E364FD4036A9C25BF357DD4  
RUN curl -o /usr/local/bin/gosu -SL
"https://github.com/tianon/gosu/releases/download/1.6/gosu-$(dpkg --print-
architecture)" \  
&& curl -o /usr/local/bin/gosu.asc -SL
"https://github.com/tianon/gosu/releases/download/1.6/gosu-$(dpkg --print-
architecture).asc" \  
&& gpg --verify /usr/local/bin/gosu.asc \  
&& rm /usr/local/bin/gosu.asc \  
&& chmod +x /usr/local/bin/gosu  
  
# Install java-8-oracle  
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-
set-selections \  
&& echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-
selections \  
&& add-apt-repository -y ppa:webupd8team/java \  
&& apt-get update \  
&& apt-get install -y --no-install-recommends \  
oracle-java8-installer ca-certificates-java \  
&& rm -rf /var/lib/apt/lists/* /var/cache/oracle-jdk8-installer/*.tar.gz
/usr/lib/jvm/java-8-oracle/src.zip /usr/lib/jvm/java-8-oracle/javafx-src.zip \  
/usr/lib/jvm/java-8-oracle/jre/lib/security/cacerts \  
&& ln -s /etc/ssl/certs/java/cacerts
/usr/lib/jvm/java-8-oracle/jre/lib/security/cacerts \  
&& update-ca-certificates  
  
# Install docker  
RUN curl -s https://get.docker.com/builds/Linux/x86_64/docker-1.11.1.tgz | tar
-xz -C /usr/local/bin --strip-components=1  
  
RUN groupadd docker && adduser --disabled-password --gecos "" teamcity \  
&& sed -i -e "s/%sudo.*$/%sudo ALL=(ALL:ALL) NOPASSWD:ALL/" /etc/sudoers \  
&& usermod -a -G docker,sudo teamcity  
  
# Install docker-compose  
RUN curl -L https://github.com/docker/compose/releases/download/1.7.0/docker-
compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose && chmod +x
/usr/local/bin/docker-compose  
  
# Install envplate  
RUN curl -L
https://github.com/kreuzwerker/envplate/releases/download/1.0.0-RC1/ep-linux
-o /usr/local/bin/ep && chmod +x /usr/local/bin/ep  
  
# Install the magic wrapper.  
ADD wrapdocker /usr/local/bin/wrapdocker  
  
ADD docker-entrypoint.sh /docker-entrypoint.sh  
  
ENTRYPOINT ["/docker-entrypoint.sh"]  
  
VOLUME /var/lib/docker  
VOLUME /opt/buildAgent  
  
EXPOSE 9090  

