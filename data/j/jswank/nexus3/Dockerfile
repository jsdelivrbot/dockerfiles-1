FROM centos:centos7  
MAINTAINER Jason Swank <docker@scalene.net>  
  
ENV NEXUS_DATA /nexus-data  
  
ENV NEXUS_VERSION 3.0.0-b2016011501  
  
ENV JAVA_HOME /opt/java  
ENV JAVA_VERSION_MAJOR 8  
ENV JAVA_VERSION_MINOR 74  
ENV JAVA_VERSION_BUILD 02  
RUN yum install -y \  
curl tar \  
&& yum clean all  
  
# install Oracle JRE  
RUN mkdir -p /opt \  
&& curl --fail --silent --location --retry 3 \  
\--header "Cookie: oraclelicense=accept-securebackup-cookie; " \  
http://download.oracle.com/otn-
pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/server-
jre-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz \  
| gunzip \  
| tar -x -C /opt \  
&& ln -s /opt/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} ${JAVA_HOME}  
  
# install nexus  
RUN mkdir -p /opt/sonatype/nexus \  
&& curl --fail --silent --location --retry 3 \  
https://download.sonatype.com/nexus/3/nexus-${NEXUS_VERSION}-unix.tar.gz \  
| gunzip \  
| tar x -C /opt/sonatype/nexus --strip-components=1 nexus-${NEXUS_VERSION} \  
&& chown -R root:root /opt/sonatype/nexus \  
&& rm -rf /tmp/nexus-${NEXUS_VERSION} \  
&& ls -laR /opt/sonatype/nexus  
  
## configure nexus runtime env  
RUN sed -e
"s|karaf.instances=data/instances|karaf.instances=${NEXUS_DATA}/instances|" -i
/opt/sonatype/nexus/bin/nexus.vmoptions  
RUN sed -e "s|karaf.data=data|karaf.data=${NEXUS_DATA}|" -i
/opt/sonatype/nexus/bin/nexus.vmoptions  
RUN sed -e "s|java.io.tmpdir=data/tmp|java.io.tmpdir=${NEXUS_DATA}/tmp|" -i
/opt/sonatype/nexus/bin/nexus.vmoptions  
  
RUN useradd -r -u 200 -m -c "nexus role account" -d ${NEXUS_DATA} -s
/bin/false nexus  
  
VOLUME ${NEXUS_DATA}  
  
EXPOSE 8081  
USER nexus  
WORKDIR /opt/sonatype/nexus  
  
ENV JAVA_MAX_MEM 768m  
ENV JAVA_MIN_MEM 256m  
ENV EXTRA_JAVA_OPTS ""  
CMD bin/nexus run  

