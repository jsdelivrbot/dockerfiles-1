FROM centos:6.7  
MAINTAINER George Liu <https://github.com/centminmod/docker-centos6-siege>  
# Setup Siege benchmark http load tester and other http load testing tools on
CentOS 6  
RUN ulimit -c -m -s -t unlimited && yum -y install dos2unix python-setuptools
python-devel libevent libevent-devel awk httpd-tools epel-release binutils
file make which nano bc traceroute mtr ping hostname wget git lynx make gcc
gcc-c++ automake screen unzip tar perl-libwww-perl perl-MIME-Base64 perl-MIME-
Base64-Perl perl-URI perl-Digest-MD5 perl-HTML-Parser perl-ExtUtils-MakeMaker
openssl openssl-devel perl-Net-SSLeay --disableplugin=fastestmirror && mkdir
-p /root/tools && yum -y install libev libev-devel libev-source; yum -y -c
http://download.opensuse.org/repositories/home:/fengshuo:/zeromq/CentOS_CentOS-6/home:fengshuo:zeromq.repo
install zeromq zeromq-devel && mkdir -p /home/tmp; export TMPDIR="/home/tmp";
easy_install locustio; easy_install pyzmq; yum -y install python-pip; pip
install -U multi-mechanize; yum clean all && rm -rf /var/cache/*  
ADD siegesetup.sh /root/tools/siegesetup.sh  
RUN dos2unix /root/tools/siegesetup.sh; chmod +x /root/tools/siegesetup.sh;
/root/tools/siegesetup.sh && yum -y update --disableplugin=fastestmirror &&
yum clean all && rm -rf /var/cache/* && echo && wrk -v ; echo; wrk2 -v ; echo;
slowhttptest -h | awk '/version / {print "slowhttptest",$13}'; echo; weighttp
-v; echo; httperf -h; echo; ab -V; echo; locust -V 2>&1 | head -n1 | awk -F ':
' '{print $2}'; echo; multimech-run -h; echo; siege -V

