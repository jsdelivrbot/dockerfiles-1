## Image name: faucet/base-pi  
FROM multiarch/alpine:armhf-v3.7  
RUN apk add --no-cache bash su-exec  
COPY entrypoint.sh /usr/local/bin/entrypoint.sh  
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]  

