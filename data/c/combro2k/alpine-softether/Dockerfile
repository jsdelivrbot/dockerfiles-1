FROM combro2k/alpine-base-glibc:latest  
  
LABEL org.label-schema.build-date=$BUILD_DATE \  
org.label-schema.vcs-ref=$VCS_REF \  
org.label-schema.vcs-url=$VCS_URL \  
org.label-scheme.dockerfile=$DOCKERFILE  
  
  
  
RUN set -xe && apk --no-cache add openssl readline ncurses curl busybox-extras
&& \  
apk \--no-cache -t .build-deps add readline-dev openssl-dev ncurses-dev build-
base cmake && \  
mkdir /tmp/softether && curl -L
https://github.com/SoftEtherVPN/SoftEtherVPN/archive/master.tar.gz | tar zvx
-C /tmp/softether --strip-components=1 && \  
cd /tmp/softether && ./configure && make -C tmp && make -C tmp install && rm
-fr /tmp/softether && \  
apk del --quiet --no-cache .build-deps && apk del --quiet --no-cache --purge
&& rm -rf /var/cache/apk/*  
  
COPY resources/ /  
  
EXPOSE 41421/udp \  
443/tcp \  
992/tcp \  
1194/tcp \  
1194/udp \  
5555/tcp \  
27088/udp \  
52651/udp  
  
VOLUME /data  
  
ENTRYPOINT ["/init"]  

