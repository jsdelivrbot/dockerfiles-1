FROM jetty:9-jre8  
  
MAINTAINER reydermanm@dnb.com  
ENV JETTY_WEBAPPS /var/lib/jetty/webapps  
ENV BLAZEGRAPH_NAME bigdata  
ENV BLAZEGRAPH_PF_PARAM com.bigdata.rdf.sail.webapp.ConfigParams.propertyFile  
ENV BLAZEGRAPH_RW_PATH /RWStore.properties  
ENV BLAZEGRAPH_VERSION 1.5.2  
ENV BLAZEGRAPH_VERSION_URL
http://sourceforge.net/projects/bigdata/files/bigdata/${BLAZEGRAPH_VERSION}/bigdata.war/download  
ADD RWStore.properties $BLAZEGRAPH_RW_PATH  
RUN wget -O ${JETTY_WEBAPPS}/${BLAZEGRAPH_NAME}.war $BLAZEGRAPH_VERSION_URL  
RUN echo "JAVA_OPTIONS='${JAVA_OPTIONS}
-D${BLAZEGRAPH_PF_PARAM}=${BLAZEGRAPH_RW_PATH}'\nJETTY_ARGS=jetty.port=80" >>
/etc/default/jetty  
RUN chown jetty:jetty $BLAZEGRAPH_RW_PATH  
RUN mkdir ${JETTY_WEBAPPS}/ROOT  
ADD app ${JETTY_WEBAPPS}/ROOT  
EXPOSE 80  
CMD ["jetty.sh", "run"]  

