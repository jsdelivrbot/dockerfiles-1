FROM node:0.10.48  
LABEL maintainer "binary4bytes@gmail.com"  
  
WORKDIR /usr/src/app  
  
COPY . /usr/src/app  
RUN npm install && npm run configure && npm run compile  
  
EXPOSE 7777  
ENV GENIEACS_MONGODB_CONNECTION_URL mongodb://mongodb/genieacs  
ENV GENIEACS_REDIS_PORT 6379  
ENV GENIEACS_REDIS_HOST redis  
ENV GENIEACS_CWMP_INTERFACE 0.0.0.0  
ENV GENIEACS_CWMP_PORT 7777  
ENV GENIEACS_CWMP_SSL false  
ENV GENIEACS_NBI_INTERFACE 0.0.0.0  
ENV GENIEACS_NBI_PORT 7777  
ENV GENIEACS_FS_INTERFACE 0.0.0.0  
ENV GENIEACS_FS_PORT 7777  
ENV GENIEACS_FS_IP 192.168.0.1  
ENV GENIEACS_LOG_INFORMS true  
ENV GENIEACS_DEBUG false  
  
# Cleanup  
RUN npm cache clear  
RUN rm -rf /root/.node-gyp /tmp/npm-*  
  
ENTRYPOINT [ "npm", "run" ]  
CMD [ "start-cwmp" ]  

