FROM centos:latest  
MAINTAINER Feng Honglin <hfeng@tutum.co>  
  
RUN yum -y install openssh-server epel-release && \  
yum -y install pwgen && \  
yum -y install sudo && \  
yum -y install firewalld firewall-config && \  
rm -f /etc/ssh/ssh_host_ecdsa_key /etc/ssh/ssh_host_rsa_key && \  
ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_ecdsa_key && \  
ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key && \  
sed -i "s/#UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g"
/etc/ssh/sshd_config && \  
sed -i "s/UsePAM.*/UsePAM yes/g" /etc/ssh/sshd_config  
  
ADD set_root_pw.sh /set_root_pw.sh  
ADD run.sh /run.sh  
RUN chmod +x /*.sh  
  
RUN localedef -i zh_TW -c -f UTF-8 zh_TW.UTF-8  
  
ENV AUTHORIZED_KEYS **None**  
  
EXPOSE 22  
CMD ["/run.sh"]  

