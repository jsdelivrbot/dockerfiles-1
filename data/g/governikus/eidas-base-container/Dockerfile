FROM governikus/zulu-openjdk:8u172  
  
MAINTAINER Benny Prange <benny.prange@governikus.de>  
  
# Define the application version for the subsequent application images  
ENV VERSION=1.0.4-rc.2  
# Define the spring boot configuration directory  
ENV CONFIG_DIR=/opt/eidas-middleware/configuration  
  
# Create a user that is the same in all application images  
RUN addgroup -S eidas-middleware && adduser -S -u 1000 -G eidas-middleware
eidas-middleware  
  
# Update and install wget to download the jar  
RUN apk --no-cache upgrade -a && \  
apk --no-cache add wget  
  
# Change owner of /opt/eidas-middleware  
RUN mkdir -p /opt/eidas-middleware &&\  
chown eidas-middleware /opt/eidas-middleware &&\  
chgrp eidas-middleware /opt/eidas-middleware  

