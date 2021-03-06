# Based on the base CentOS 7.2.1511 image, create an image customized as a  
# Jenkins SSH slave.  
FROM centos:7.2.1511  
MAINTAINER David Filion <filiond@gmail.com>  
  
  
# Allow the specification of http(s) proxys.  
ARG http_proxy  
ARG https_proxy  
  
  
# Deal with Docker language issues.  
COPY C.utf8 /usr/lib/locale/C.utf8  
ENV LANG C.UTF-8  
# Install required packages  
RUN yum install -y epel-release \  
&& yum install -y \  
ansible \  
git \  
java-1.8.0-openjdk-headless \  
openssh-server \  
sudo \  
which \  
&& yum clean all  
  
# Due to a kernel bug,  
RUN rm -rf /etc/ld.so.cache \  
&& rm -rf /sbin/sln \  
&& rm -rf /usr/share/man \  
&& rm -rf /usr/share/doc \  
&& rm -rf /usr/share/info \  
&& rm -rf /usr/share/gnome/help \  
&& rm -rf /usr/share/cracklib \  
&& rm -rf /{root,tmp,var/cache/{ldconfig,yum}}/*  
  
# Add Mercurial support.  
RUN /usr/bin/yum -y localinstall https://www.mercurial-
scm.org/release/centos7/RPMS/x86_64/mercurial-3.4.2-0.x86_64.rpm  
  
# Fix SSH's PAM configuration so we can login.  
RUN sed -i 's|session required pam_loginuid.so|session optional
pam_loginuid.so|g' /etc/pam.d/sshd  
  
# Update sudo setup.  
RUN sed -i 's|Defaults requiretty|#Defaults requiretty|' /etc/sudoers \  
&& echo 'Defaults env_keep += "http_proxy https_proxy"' >> /etc/sudoers \  
&& echo '%users ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers  
  
# Configure timezone  
RUN ln -sf \  
/usr/share/zoneinfo/UTC \  
/etc/localtime \  
&& echo "NETWORKING=yes" > /etc/sysconfig/network  
  
# Setup the jenkins user. Unlike a standard jenkins install, we give Jenkins  
# a shell so it can login.  
RUN useradd -d /var/lib/jenkins -m -s /bin/bash -c "Jenkins Continuous Build
Account" jenkins  
RUN echo "jenkins:jenkins" | chpasswd  
  
EXPOSE 22  
RUN /usr/bin/ssh-keygen -A  
  
CMD ["/usr/sbin/sshd", "-D"]  
  

