FROM debian:jessie-backports as builder  
  
# add our user and group first to make sure their IDs get assigned
consistently, regardless of whatever dependencies get added  
#RUN groupadd -r www-data && useradd -r --create-home -g www-data www-data  
  
ENV HTTPD_PREFIX /usr/local/apache2  
ENV PATH $HTTPD_PREFIX/bin:$PATH  
RUN mkdir -p "$HTTPD_PREFIX" \  
&& chown www-data:www-data "$HTTPD_PREFIX"  
WORKDIR $HTTPD_PREFIX  
# library for mod_http2  
ENV NGHTTP2_VERSION 1.18.1-1  
ENV OPENSSL_VERSION 1.0.2l-1~bpo8+1  
RUN { \  
echo 'deb http://deb.debian.org/debian stretch main'; \  
} > /etc/apt/sources.list.d/stretch.list \  
&& { \  
# add a negative "Pin-Priority" so that we never ever get packages from
stretch unless we explicitly request them  
echo 'Package: *'; \  
echo 'Pin: release n=stretch'; \  
echo 'Pin-Priority: -10'; \  
echo; \  
# except nghttp2, which is the reason we're here  
echo 'Package: libnghttp2*'; \  
echo "Pin: version $NGHTTP2_VERSION"; \  
echo 'Pin-Priority: 990'; \  
echo; \  
} > /etc/apt/preferences.d/unstable-nghttp2  
  
# install httpd runtime dependencies  
# https://httpd.apache.org/docs/2.4/install.html#requirements  
RUN apt-get update \  
&& apt-get install -y --no-install-recommends \  
libapr1 \  
libaprutil1 \  
libaprutil1-ldap \  
libapr1-dev \  
libaprutil1-dev \  
liblua5.2-0 \  
libnghttp2-14=$NGHTTP2_VERSION \  
libpcre++0 \  
libssl1.0.0=$OPENSSL_VERSION \  
libxml2 \  
&& rm -r /var/lib/apt/lists/*  
  
ENV HTTPD_VERSION 2.4.33  
ENV HTTPD_SHA256
de02511859b00d17845b9abdd1f975d5ccb5d0b280c567da5bf2ad4b70846f05  
  
# https://httpd.apache.org/security/vulnerabilities_24.html  
ENV HTTPD_PATCHES=""  
  
ENV APACHE_DIST_URLS \  
#
https://issues.apache.org/jira/browse/INFRA-8753?focusedCommentId=14735394#comment-14735394  
https://www.apache.org/dyn/closer.cgi?action=download&filename= \  
# if the version is outdated (or we're grabbing the .asc file), we might have
to pull from the dist/archive :/  
https://www-us.apache.org/dist/ \  
https://www.apache.org/dist/ \  
https://archive.apache.org/dist/  
  
# see https://httpd.apache.org/docs/2.4/install.html#requirements  
RUN set -eux; \  
\  
# mod_http2 mod_lua mod_proxy_html mod_xml2enc  
# https://anonscm.debian.org/cgit/pkg-
apache/apache2.git/tree/debian/control?id=adb6f181257af28ee67af15fc49d2699a0080d4c  
buildDeps=" \  
bzip2 \  
ca-certificates \  
dpkg-dev \  
gcc \  
liblua5.2-dev \  
libnghttp2-dev=$NGHTTP2_VERSION \  
libpcre++-dev \  
libssl-dev=$OPENSSL_VERSION \  
libxml2-dev \  
zlib1g-dev \  
make \  
wget \  
cmake \  
build-essential \  
"; \  
apt-get update; \  
apt-get install -y --no-install-recommends -V $buildDeps; \  
rm -r /var/lib/apt/lists/*; \  
mkdir -p brotli; \  
wget https://github.com/google/brotli/archive/v1.0.3.tar.gz; \  
tar -xzf v1.0.3.tar.gz -C brotli --strip-components=1; \  
rm v1.0.3.tar.gz; \  
cd brotli; \  
mkdir out; \  
cd out; \  
../configure-cmake --disable-debug; \  
make; \  
make test; \  
make install; \  
cd ../.. ; \  
rm -rf brotli; \  
\  
ddist() { \  
local f="$1"; shift; \  
local distFile="$1"; shift; \  
local success=; \  
local distUrl=; \  
for distUrl in $APACHE_DIST_URLS; do \  
if wget -O "$f" "$distUrl$distFile" && [ -s "$f" ]; then \  
success=1; \  
break; \  
fi; \  
done; \  
[ -n "$success" ]; \  
}; \  
\  
ddist 'httpd.tar.bz2' "httpd/httpd-$HTTPD_VERSION.tar.bz2"; \  
echo "$HTTPD_SHA256 *httpd.tar.bz2" | sha256sum -c -; \  
\  
# see https://httpd.apache.org/download.cgi#verify  
ddist 'httpd.tar.bz2.asc' "httpd/httpd-$HTTPD_VERSION.tar.bz2.asc"; \  
export GNUPGHOME="$(mktemp -d)"; \  
for key in \  
# gpg: key 791485A8: public key "Jim Jagielski (Release Signing Key)
<jim@apache.org>" imported  
A93D62ECC3C8EA12DB220EC934EA76E6791485A8 \  
# gpg: key 995E35221AD84DFF: public key "Daniel Ruggeri
(http://home.apache.org/~druggeri/) <druggeri@apache.org>" imported  
B9E8213AEFB861AF35A41F2C995E35221AD84DFF \  
; do \  
gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \  
done; \  
gpg --batch --verify httpd.tar.bz2.asc httpd.tar.bz2; \  
rm -rf "$GNUPGHOME" httpd.tar.bz2.asc; \  
\  
mkdir -p src; \  
tar -xf httpd.tar.bz2 -C src --strip-components=1; \  
rm httpd.tar.bz2; \  
cd src; \  
\  
patches() { \  
while [ "$#" -gt 0 ]; do \  
local patchFile="$1"; shift; \  
local patchSha256="$1"; shift; \  
ddist "$patchFile" "httpd/patches/apply_to_$HTTPD_VERSION/$patchFile"; \  
echo "$patchSha256 *$patchFile" | sha256sum -c -; \  
patch -p0 < "$patchFile"; \  
rm -f "$patchFile"; \  
done; \  
}; \  
patches $HTTPD_PATCHES; \  
\  
gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)"; \  
./configure \  
\--build="$gnuArch" \  
\--prefix="$HTTPD_PREFIX" \  
\--enable-mods-shared=reallyall \  
\--with-pcre=/usr/bin/pcre-config --enable-ssl --enable-so --enable-brotli
--with-brotli=/usr/local/brotli \  
\--enable-mpms-shared=all \  
; \  
make -j "$(nproc)"; \  
make install; \  
\  
cd ..; \  
rm -r src man manual; \  
\  
sed -ri \  
-e 's!^(\s*CustomLog)\s+\S+!\1 /proc/self/fd/1!g' \  
-e 's!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g' \  
"$HTTPD_PREFIX/conf/httpd.conf"; \  
\  
apt-get purge -y --auto-remove $buildDeps  
  
  
FROM eeacms/apache:2.4-2.3  
LABEL maintainer="European Environment Agency (EEA): IDM2 A-Team <eea-edw-a-
team-alerts@googlegroups.com>"  
  
ENV APACHE_MODULES="http2_module mime_magic_module data_module
unique_id_module remoteip_module negotiation_module brotli_module" \  
APACHE_INCLUDE="conf/extra/httpd-languages.conf conf/extra/httpd-default.conf"
\  
APACHE_TIMEOUT="120" \  
APACHE_KEEPALIVE_TIMEOUT="8"  
  
  
COPY src/* /tmp/  
  
RUN runDeps=" curl libsys-syslog-perl apt-transport-https ca-certificates" \  
&& apt-get update \  
&& apt-get install -y --no-install-recommends $runDeps \  
&& mkdir -p /usr/local/apache2/conf/extra/ /var/eea-buildout-plone4/etc/apache
/var/eea-buildout-plone4/etc/scripts /var/local/www-logs/eea /var/www/html
/var/www-static-resources/ \  
&& sed -i 's|ServerName eeacms-apache.docker.com|ServerName
www.eea.europa.eu|' /usr/local/apache2/conf/httpd.conf \  
&& sed -i 's|you@example.com|helpdesk@eea.europa.eu|'
/usr/local/apache2/conf/httpd.conf \  
&& mv /tmp/apache_syslog /var/eea-buildout-plone4/etc/scripts/ \  
&& mv /tmp/vh-www-common.inc /var/eea-buildout-plone4/etc/apache/ \  
&& mv /tmp/vh-www-https.conf /var/eea-buildout-plone4/etc/apache/ \  
&& mv /tmp/vh-wwwplone.conf /usr/local/apache2/conf/extra/ \  
&& mv /docker-entrypoint.sh /apache-entrypoint.sh  
  
COPY --from=builder /usr/local/apache2/modules/mod_brotli.so
/usr/local/apache2/modules/  
COPY --from=builder /usr/local/bin/brotli /usr/local/bin/brotli  
COPY --from=builder /usr/local/lib/libbrotli* /usr/local/lib/  
COPY --from=builder /usr/local/include/brotli /usr/local/include/  
COPY --from=builder /usr/local/lib/pkgconfig/libbrotli*
/usr/local/lib/pkgconfig/  
  
  
  
COPY docker-entrypoint.sh /  

