# Download base image  
FROM alpine:3.4  
MAINTAINER Quinn D Granfor, spootdev@gmail.com  
  
LABEL www.mediakraken.org.version="dev-0.2.0"  
LABEL Description="This image scans for new hardware devices"  
  
RUN mkdir /mediakraken  
WORKDIR /mediakraken  
  
# add hdhomerun lib to install  
ADD PyHdHomeRun /mediakraken/PyHdHomeRun  
ADD libhdhomerun /mediakraken/libhdhomerun  
ADD libhdhomerun_python /mediakraken/libhdhomerun_python  
  
# Update repository and install packages  
RUN apk add --update \  
python \  
alpine-sdk \  
py-setuptools \  
python-dev \  
&& cd libhdhomerun \  
&& make \  
&& cd .. \  
&& mv ./libhdhomerun/hdhomerun_config . \  
&& mv ./libhdhomerun/libhdhomerun.so /usr/lib/. \  
&& mv libhdhomerun /usr/include/. \  
&& cd PyHdHomeRun \  
&& python setup.py install \  
&& cd .. \  
&& rm -R PyHdHomeRun \  
&& cd libhdhomerun_python \  
&& python setup.py install \  
&& cd .. \  
&& rm -R libhdhomerun_python \  
&& rm -R /usr/include/libhdhomerun \  
&& apk del alpine-sdk \  
python-dev \  
&& rm -rf /var/cache/apk/*  
  
# Copy the source files for the app  
ADD src /mediakraken  
  
CMD ["/bin/ash"]  
  

