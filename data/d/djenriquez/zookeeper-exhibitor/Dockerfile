FROM debian:7.8  
MAINTAINER DJ Enriquez <dj@glympse.com>  
  
ENV ZK_VERSION 3.4.9  
ENV ZK_RELEASE
http://www.apache.org/dist/zookeeper/zookeeper-${ZK_VERSION}/zookeeper-${ZK_VERSION}.tar.gz  
ENV EXHIBITOR_POM
https://raw.githubusercontent.com/Netflix/exhibitor/d911a16d704bbe790d84bbacc655ef050c1f5806/exhibitor-
standalone/src/main/resources/buildscripts/standalone/maven/pom.xml  
ENV DEBIAN_FRONTEND noninteractive  
  
# Use one step so we can remove intermediate dependencies and minimize size  
RUN \  
# Install dependencies  
apt-get update && \  
apt-get install -y --allow-unauthenticated --no-install-recommends curl maven
openjdk-7-jdk+  
  
# Default DNS cache TTL is -1. DNS records, like, change, man.  
RUN \  
grep '^networkaddress.cache.ttl=' /etc/java-7-openjdk/security/java.security
|| echo 'networkaddress.cache.ttl=60' >>
/etc/java-7-openjdk/security/java.security  
  
# Install ZK  
RUN \  
curl -Lo /tmp/zookeeper.tgz $ZK_RELEASE \  
&& mkdir -p /opt/zookeeper/transactions /opt/zookeeper/snapshots \  
&& tar -xzf /tmp/zookeeper.tgz -C /opt/zookeeper --strip=1 \  
&& rm /tmp/zookeeper.tgz  
  
# Install Exhibitor  
RUN \  
mkdir -p /opt/exhibitor \  
&& curl -Lo /opt/exhibitor/pom.xml $EXHIBITOR_POM \  
&& mvn -f /opt/exhibitor/pom.xml package \  
&& ln -s /opt/exhibitor/target/exhibitor*jar /opt/exhibitor/exhibitor.jar \  
  
# Remove build-time dependencies  
&& apt-get purge -y --auto-remove maven openjdk-7-jdk+ \  
&& rm -rf /var/lib/apt/lists/*  
  
# Add the wrapper script to setup configs and exec exhibitor  
ADD include/wrapper.sh /opt/exhibitor/wrapper.sh  
  
# Add the optional web.xml for authentication  
ADD include/web.xml /opt/exhibitor/web.xml  
  
USER root  
WORKDIR /opt/exhibitor  
EXPOSE 2181 2888 3888 8181  
ENTRYPOINT ["bash", "-ex", "/opt/exhibitor/wrapper.sh"]

