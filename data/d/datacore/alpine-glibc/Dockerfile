FROM registry.timmertech.nl/docker/alpine-base:latest  
  
ARG BUILD_DATE  
ARG VCS_REF  
  
LABEL \  
maintainer="G.J.R. Timmer <gjr.timmer@gmail.com>" \  
nl.timmertech.build-date=${BUILD_DATE} \  
nl.timmertech.name=alpine-glibc \  
nl.timmertech.vendor=timmertech.nl \  
nl.timmertech.vcs-url="https://github.com/GJRTimmer/docker-alpine-glibc.git" \  
nl.timmertech.vcs-ref=${VCS_REF} \  
nl.timmertech.license=MIT  
  
ENV LANG=C.UTF-8  
ENV ALPINE_GLIBC_PACKAGE_VERSION=2.27-r0  
  
RUN ALPINE_GLIBC_BASE_URL="https://github.com/sgerrand/alpine-pkg-
glibc/releases/download" && \  
ALPINE_GLIBC_BASE_PACKAGE_FILENAME="glibc-$ALPINE_GLIBC_PACKAGE_VERSION.apk"
&& \  
ALPINE_GLIBC_BIN_PACKAGE_FILENAME="glibc-
bin-$ALPINE_GLIBC_PACKAGE_VERSION.apk" && \  
ALPINE_GLIBC_I18N_PACKAGE_FILENAME="glibc-i18n-$ALPINE_GLIBC_PACKAGE_VERSION.apk"
&& \  
apk add \--no-cache \--virtual=.build-dependencies wget ca-certificates && \  
wget \  
"https://raw.githubusercontent.com/sgerrand/alpine-pkg-
glibc/master/sgerrand.rsa.pub" \  
-O "/etc/apk/keys/sgerrand.rsa.pub" && \  
wget \  
"$ALPINE_GLIBC_BASE_URL/$ALPINE_GLIBC_PACKAGE_VERSION/$ALPINE_GLIBC_BASE_PACKAGE_FILENAME"
\  
"$ALPINE_GLIBC_BASE_URL/$ALPINE_GLIBC_PACKAGE_VERSION/$ALPINE_GLIBC_BIN_PACKAGE_FILENAME"
\  
"$ALPINE_GLIBC_BASE_URL/$ALPINE_GLIBC_PACKAGE_VERSION/$ALPINE_GLIBC_I18N_PACKAGE_FILENAME"
&& \  
apk add \--no-cache \  
"$ALPINE_GLIBC_BASE_PACKAGE_FILENAME" \  
"$ALPINE_GLIBC_BIN_PACKAGE_FILENAME" \  
"$ALPINE_GLIBC_I18N_PACKAGE_FILENAME" && \  
rm "/etc/apk/keys/sgerrand.rsa.pub" && \  
/usr/glibc-compat/bin/localedef --force --inputfile POSIX --charmap UTF-8
"$LANG" || true && \  
echo "export LANG=$LANG" > /etc/profile.d/locale.sh && \  
apk del glibc-i18n && \  
rm "/root/.wget-hsts" && \  
apk del .build-dependencies && \  
rm "$ALPINE_GLIBC_BASE_PACKAGE_FILENAME" \  
"$ALPINE_GLIBC_BIN_PACKAGE_FILENAME" \  
"$ALPINE_GLIBC_I18N_PACKAGE_FILENAME"  
# EOF

