FROM bitnami/minideb:jessie as buildenv  
  
RUN install_packages ca-certificates wget  
RUN wget -nc -P /tmp/bitnami/pkg/cache/
https://downloads.bitnami.com/files/stacksmith/service-
catalog-0.1.21-0-linux-x64-debian-8.tar.gz && \  
echo "52e4d45f09e492c94d6af69ce5756b4d19ff7227a9a57f507f67b77be8ad624f
/tmp/bitnami/pkg/cache/service-catalog-0.1.21-0-linux-x64-debian-8.tar.gz" |
sha256sum -c - && \  
tar -zxf /tmp/bitnami/pkg/cache/service-
catalog-0.1.21-0-linux-x64-debian-8.tar.gz -P --transform
's|^[^/]*/files|/opt/bitnami|' \--wildcards '*/files' && \  
rm -rf /tmp/bitnami/pkg/cache/service-
catalog-0.1.21-0-linux-x64-debian-8.tar.gz  
  
##################  
FROM bitnami/minideb:jessie  
LABEL maintainer "Bitnami <containers@bitnami.com>"  
  
COPY \--from=buildenv /opt/bitnami/service-catalog /opt/bitnami/service-
catalog  
ENV BITNAMI_APP_NAME="service-catalog" \  
BITNAMI_IMAGE_VERSION="0.1.21-r3" \  
PATH="/opt/bitnami/service-catalog/bin:$PATH"  
EXPOSE 8443 443  
WORKDIR /opt/bitnami/service-catalog  
USER 1001  
ENTRYPOINT ["/opt/bitnami/service-catalog/bin/service-catalog"]  

