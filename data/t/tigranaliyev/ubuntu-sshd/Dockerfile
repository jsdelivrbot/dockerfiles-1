FROM ubuntu:16.04  
MAINTAINER Aleksandar Diklic "https://github.com/rastasheep"  
RUN apt-get update  
  
RUN apt-get install -y openssh-server  
RUN mkdir /var/run/sshd  
  
RUN echo 'root:root' |chpasswd  
  
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/'
/etc/ssh/sshd_config  
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config  
RUN sed -ri 's/Port 22/Port 80/g' /etc/ssh/sshd_config  
  
EXPOSE 80  
CMD ["/usr/sbin/sshd", "-D"]  

