FROM ubuntu:14.04  
  
RUN set -x \  
&& echo "deb http://ubuntu.kurento.org trusty kms6" | tee
/etc/apt/sources.list.d/kurento.list \  
&& apt-key adv --keyserver keyserver.ubuntu.com --recv 2F819BC0 \  
&& apt-get update \  
&& apt-get -y dist-upgrade \  
&& apt-get -y install \  
kurento-media-server-6.0 \  
kms-chroma-6.0 \  
kms-crowddetector-6.0 \  
kms-platedetector-6.0 \  
kms-pointerdetector-6.0  
#RUN apt-get install -y \  
# gdb \  
# kurento-media-server-6.0-dbg \  
# kms-core-6.0-dbg \  
# kms-elements-6.0-dbg \  
# kms-filters-6.0-dbg \  
# kms-chroma-6.0-dbg \  
# kms-crowddetector-6.0-dbg \  
# kms-platedetector-6.0-dbg \  
# kms-pointerdetector-6.0-dbg \  
# gstreamer1.5-libav-dbg \  
# gstreamer1.5-plugins-bad-dbg \  
# gstreamer1.5-plugins-base-dbg \  
# gstreamer1.5-plugins-good-dbg \  
# gstreamer1.5-plugins-ugly-dbg \  
# kms-jsonrpc-1.0-dbg \  
# kmsjsoncpp-dbg \  
# libglib2.0-0-dbg \  
# libgstreamer1.5-0-dbg \  
# libnice-dbg \  
# openwebrtc-gst-plugins-dbg \  
# && apt-get clean \  
# && rm -rf /var/lib/apt/lists/*  
  
ENV GST_DEBUG=Kurento*:5  
  
COPY ./docker-entrypoint.sh /bin/docker-entrypoint.sh  
RUN chmod +x /bin/docker-entrypoint.sh  
  
EXPOSE 8888  
ENTRYPOINT ["/bin/docker-entrypoint.sh"]  

