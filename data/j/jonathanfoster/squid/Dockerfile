FROM alpine:latest  
  
RUN apk add --no-cache squid apache2-utils  
  
COPY squid.conf /etc/squid/  
  
EXPOSE 3128  
ENTRYPOINT ["/usr/sbin/squid"]  
CMD ["-NYCd", "1"]  

