# This Dockerfile is used to build an sakuli image based on Ubuntu  
FROM ubuntu:16.04  
MAINTAINER Robert Bohne "Robert.Bohne@ConSol.de"  
ENV REFRESHED_AT 2016-08-11  
LABEL io.k8s.description="Headless VNC Container with icewm, firefox and
chromium" \  
io.k8s.display-name="Headless VNC Container" \  
io.openshift.expose-services="6901:http,5901:xvnc" \  
io.openshift.tags="vnc, sakuli" \  
io.openshift.non-scalable=true  
  
ENV JAVA_VERSION 8u92  
ENV JAVA_HOME /usr/lib/jvm/java-$JAVA_VERSION  
  
ENV DEBIAN_FRONTEND noninteractive  
ENV DISPLAY :1  
ENV NO_VNC_HOME /headless/noVNC  
ENV VNC_COL_DEPTH 24  
ENV VNC_RESOLUTION 1280x1024  
ENV VNC_PW vncpassword  
  
ENV SAKULI_DOWNLOAD_URL https://labs.consol.de/sakuli/install  
  
############### add linux-mint dependicies and update packages  
RUN apt-key adv --recv-key --keyserver keyserver.ubuntu.com "3EE67F3D0FF405B2"  
RUN echo "deb http://packages.linuxmint.com/ rafaela main upstream import" >>
/etc/apt/sources.list.d/mint.list \  
&& echo "deb http://extra.linuxmint.com/ rafaela main " >>
/etc/apt/sources.list.d/mint.list  
  
############### xvnc / xfce installation  
RUN apt-get update && \  
apt-get upgrade -y && \  
apt-get install -y supervisor vim icewm vnc4server wget libnss-wrapper gettext
net-tools xterm && \  
apt-get clean -y  
  
### Install noVNC - HTML5 based VNC viewer  
RUN mkdir -p $NO_VNC_HOME/utils/websockify &&\  
wget -qO- https://github.com/ConSol/noVNC/archive/consol_1.0.0.tar.gz | tar xz
--strip 1 -C $NO_VNC_HOME &&\  
wget -qO- https://github.com/kanaka/websockify/archive/v0.7.0.tar.gz | tar xz
--strip 1 -C $NO_VNC_HOME/utils/websockify &&\  
chmod +x -v /headless/noVNC/utils/*.sh  
  
### Install firfox and chrome browser  
RUN apt-get install -y firefox chromium-browser chromium-browser-l10n
chromium-codecs-ffmpeg &&\  
apt-get clean -y &&\  
ln -s /usr/bin/chromium-browser /usr/bin/google-chrome &&\  
echo "CHROMIUM_FLAGS='--no-sandbox --start-maximized --user-data-dir'" >
/headless/.chromium-browser.init  
  
##### Add Oracle JAVA JRE8  
RUN mkdir -p $JAVA_HOME &&\  
# download and extract  
wget -qO- $SAKULI_DOWNLOAD_URL/3rd-party/java/jre-$JAVA_VERSION-
linux-x64.tar.gz | tar xz --strip 1 -C $JAVA_HOME &&\  
# set alternatives  
update-alternatives --install "/usr/bin/java" "java" "$JAVA_HOME/bin/java" 1
&&\  
update-alternatives --install "/usr/bin/javaws" "javaws"
"$JAVA_HOME/bin/javaws" 1 &&\  
update-alternatives --install "/usr/lib/firefox/browser/plugins/mozilla-
javaplugin.so" "mozilla-javaplugin.so" "$JAVA_HOME/lib/amd64/libnpjp2.so" 1  
# xvnc server porst, if $DISPLAY=:1 port will be 5901  
EXPOSE 5901  
# novnc web port  
EXPOSE 6901  
ENV HOME /headless  
  
ADD .icewm /headless/.icewm  
ADD scripts /headless/scripts  
  
RUN chmod +x /headless/scripts/*.sh  
RUN chgrp -R 0 /headless  
RUN chmod -R g+rw /headless  
RUN find /headless -type d -exec chmod g+x {} +  
  
USER 1984  
ENTRYPOINT ["/headless/scripts/vnc_startup.sh"]  
CMD ["--tail-log"]  

