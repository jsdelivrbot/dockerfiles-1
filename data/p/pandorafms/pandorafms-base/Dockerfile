FROM centos:centos6  
MAINTAINER Pandora FMS Team <info@pandorafms.com>  
  
RUN { \  
echo '[EPEL]'; \  
echo 'name = CentOS Epel'; \  
echo 'baseurl = http://dl.fedoraproject.org/pub/epel/6/x86_64'; \  
echo 'enabled=1'; \  
echo 'gpgcheck=0'; \  
} > /etc/yum.repos.d/extra_repos.repo  
  
RUN { \  
echo '[artica_pandorafms]'; \  
echo 'name=CentOS6 - PandoraFMS official repo'; \  
echo 'baseurl=http://artica.es/centos6'; \  
echo 'gpgcheck=0'; \  
echo 'enabled=1'; \  
} > /etc/yum.repos.d/pandorafms.repo  
  
RUN yum -y update; yum clean all;  
  
# Generic dependencies  
RUN yum install -y \  
firefox \  
python-pip \  
xorg-x11-server-Xvfb; yum clean all;  
RUN pip install pyvirtualdisplay  
RUN pip install 'selenium==2.53.0'  
RUN pip install unittest2  
RUN pip install testtools  
  
# Pandora FMS Console dependencies  
RUN yum install -y \  
git \  
httpd \  
cronie \  
ntp \  
openldap \  
nfdump \  
wget \  
curl \  
openldap \  
plymouth \  
xterm \  
php \  
php-gd \  
graphviz \  
php-mysql \  
php-pear-DB \  
php-pear \  
php-pdo \  
php-mbstring \  
php-ldap \  
php-snmp \  
php-ldap \  
php-common \  
php-zip \  
nmap \  
xprobe2 \  
mysql-server \  
mysql; yum clean all;  
  
# Pandora FMS Server dependencies  
RUN yum install -y \  
git \  
cronie \  
ntp \  
wget \  
nano \  
curl \  
xterm \  
postfix \  
wmic \  
perl-HTML-Tree \  
perl-DBI \  
perl-DBD-mysql \  
perl-libwww-perl \  
perl-XML-Simple \  
perl-XML-SAX \  
perl-NetAddr-IP \  
perl-Scope-Guard \  
net-snmp \  
net-tools \  
perl-IO-Socket-INET6 \  
perl-Socket6 \  
nmap \  
sudo \  
xprobe2 \  
make \  
perl-CPAN \  
perl-JSON \  
net-snmp-perl \  
perl-Time-HiRes \  
perl-XML-Twig \  
perl-Encode-Locale \  
net-snmp \  
net-snmp-utils \  
perl-Test-Simple; yum clean all;  
  
RUN wget
http://rpmfind.net/linux/centos/6.9/os/i386/Packages/gettext-0.17-18.el6.i686.rpm;
\  
yum localinstall -y gettext-0.17-18.el6.i686.rpm; \  
rm -rf gettext-0.17-18.el6.i686.rpm;  
  
#Exposing ports for: HTTP, SNMP Traps, Tentacle protocol  
EXPOSE 80 162/udp 41121  

