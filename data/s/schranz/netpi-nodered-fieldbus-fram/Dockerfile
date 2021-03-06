#use latest armv7hf compatible debian version from group resin.io as base
image  
FROM resin/armv7hf-debian:stretch  
  
#enable building ARM container on x86 machinery on the web (comment out next
line if built on Raspberry)  
RUN [ "cross-build-start" ]  
  
#labeling  
LABEL maintainer="netpi@hilscher.com" \  
version="V1.0.0.0" \  
description="Node-RED with Fieldbus Nodes for netPI RTE 3 (and Pi 3 + NHAT
52-RTE)"  
#version  
ENV HILSCHERNETPI_NODERED_FB_VERSION 1.0.0.0  
#copy files  
COPY "./init.d/*" /etc/init.d/  
COPY "./node-red-contrib-fieldbus/*" "./node-red-contrib-fieldbus/lib/*"
"./firmwares/*" "./driver/*" "./web-configurator-fieldbus/*" /tmp/  
COPY "./node-red-contrib-fram/*" /tmp/fram/  
  
#do installation  
RUN apt-get update \  
&& apt-get install curl libboost-filesystem1.62-dev libboost-date-time1.62-dev
libjansson-dev p7zip-full build-essential python-dev \  
#install node.js V8.x.x  
&& curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash - \  
&& apt-get install -y nodejs \  
#install Node-RED  
&& npm install -g --unsafe-perm node-red \  
#install netx driver  
&& dpkg -i /tmp/netx-docker-pi-drv-1.1.3.deb \  
#compile program checking whether we are running on netPI RTE 3 or on Pi with
NHAT 52-RTE  
&& mv /tmp/checkdevicetype.c /opt/cifx \  
&& gcc /opt/cifx/checkdevicetype.c -o /opt/cifx/checkdevicetype -I
/usr/include/cifx -lcifx \  
&& chmod +x /opt/cifx/checkdevicetype \  
#install web fieldbus configurator  
&& 7z -t7z -r -v: x "/tmp/WebConfigurator_V1.0200.960.7z"
-o/usr/lib/node_modules \  
&& mv "/usr/lib/node_modules/WebConfigurator V1.0200.960"
"/usr/lib/node_modules/WebConfigurator" \  
&& cd /usr/lib/node_modules/WebConfigurator/ServerContent/ \  
&& npm install \  
#make some changes in the fielbus configurator setup file  
&& sed -i -e 's;"uiHost": "127.0.0.1";\"uiHost": "";' ServerSettings.json \  
&& sed -i -e 's;"configuration-file-path": "/opt/node-
red/.userdir";\"configuration-file-path": "/root/.node-red/";'
ServerSettings.json \  
&& sed -i -e 's;"platform": "";\"platform": "npi3";' ServerSettings.json \  
#install fieldbus nodes  
&& mkdir /root/.node-red \  
&& mv /tmp/fieldbusSettings.json /root/.node-red \  
&& mkdir /usr/lib/node_modules/node-red/nodes/hilscher
/usr/lib/node_modules/node-red/nodes/hilscher/fieldbus
/usr/lib/node_modules/node-red/nodes/hilscher/fieldbus/lib \  
&& mv /tmp/10-fieldbus.html /tmp/10-fieldbus.js /tmp/package.json -t
/usr/lib/node_modules/node-red/nodes/hilscher/fieldbus \  
&& mv /tmp/fieldbusConnectionPool.js /tmp/fieldbusHandler.js
/tmp/HilscherLog.js /tmp/HilscherToolBox.js /usr/lib/node_modules/node-
red/nodes/hilscher/fieldbus/lib \  
&& cd /usr/lib/node_modules/node-red/nodes/hilscher/fieldbus \  
&& npm install \  
#install fieldbus nodes wrapper library and generate needed libboost V1.61.0
links  
&& mv /tmp/fieldbus.node /usr/lib/node_modules/node-
red/nodes/hilscher/fieldbus/lib \  
&& ln -s /usr/lib/arm-linux-gnueabihf/libboost_filesystem.so.1.62.0
/usr/lib/arm-linux-gnueabihf/libboost_filesystem.so.1.61.0 \  
&& ln -s /usr/lib/arm-linux-gnueabihf/libboost_system.so.1.62.0 /usr/lib/arm-
linux-gnueabihf/libboost_system.so.1.61.0 \  
#install netx firmwares from zip  
&& mkdir /opt/cifx/deviceconfig/FW/channel0 \  
&& 7z -tzip -r -v: x "/tmp/FWPool.zip" -o/root/.node-red \  
#install fram nodes  
&& mkdir /usr/lib/node_modules/node-red-contrib-fram \  
&& mv /tmp/fram/fram.js /tmp/fram/fram.html /tmp/fram/package.json -t
/usr/lib/node_modules/node-red-contrib-fram \  
&& cd /usr/lib/node_modules/node-red-contrib-fram \  
&& npm install \  
#install ssh  
&& apt-get install -y git openssh-server \  
&& echo 'root:root' | chpasswd \  
&& sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/'
/etc/ssh/sshd_config \  
&& sed 's@session\s*required\s*pam_loginuid.so@session optional
pam_loginuid.so@g' -i /etc/pam.d/sshd \  
&& mkdir /var/run/sshd \  
#clean up  
&& rm -rf /tmp/* \  
&& apt-get remove p7zip-full curl \  
&& apt-get -yqq autoremove \  
&& apt-get -y clean \  
&& rm -rf /var/lib/apt/lists/*  
#set the entrypoint  
ENTRYPOINT ["/etc/init.d/entrypoint.sh"]  
  
#Node-RED and fieldbus web configurator ports  
EXPOSE 1880 9000 22  
#set STOPSGINAL  
STOPSIGNAL SIGTERM  
  
#stop processing ARM emulation (comment out next line if built on Raspberry)  
RUN [ "cross-build-end" ]  

