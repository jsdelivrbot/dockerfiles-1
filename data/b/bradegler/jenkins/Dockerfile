FROM bradegler/java7  
MAINTAINER Brad Egler "begler@gmail.com"  
RUN echo deb http://pkg.jenkins-ci.org/debian binary/ >
/etc/apt/sources.list.d/jenkins.list  
RUN wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | apt-key
add -  
RUN apt-get -yq update && apt-get -yq upgrade  
RUN apt-get -yq install jenkins=`apt-cache madison jenkins | head -1 | cut -d
\| -f 2 | tr -d ' '`  
  
USER jenkins  
ENV HOME /var/lib/jenkins  
WORKDIR /var/lib/jenkins  
ADD run_jenkins.sh /usr/share/jenkins/run_jenkins.sh  
  
VOLUME /var/lib/jenkins-jobs  
  
EXPOSE 8080  
CMD ["/usr/share/jenkins/run_jenkins.sh"]  

