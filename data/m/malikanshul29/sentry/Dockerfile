# Sentry dev environment  
#  
# NOTE: This should not be used in production!  
#  
# Instructions:  
#  
# Build the container:  
# $ docker build --rm -t sentry:dev -f Dockerfile.dev .  
# Bootstrap the container:  
# $ docker run --name=sentry-dev -p 8000:8000 -it -v $PWD:/usr/src/sentry
sentry:dev  
# Run the container:  
# $ docker start sentry-dev  
# Attach into the container:  
# $ docker exec -it sentry-dev bash  
# Run devserver:  
# $ docker exec -it sentry-dev sentry devserver 0.0.0.0:8000  
# Stop container:  
# $ docker stop sentry-dev  
# Remove container:  
# $ docker rm -f sentry-dev  
#  
FROM python:2.7.11-slim  
  
RUN groupadd -r memcached --gid=997 && useradd -r -g memcached --uid=997
memcached \  
&& groupadd -r redis --gid=998 && useradd -r -g redis --uid=998 redis \  
&& groupadd -r postgres --gid=999 && useradd -r -g postgres --uid=999 postgres  
  
RUN apt-get update && apt-get install -y --no-install-recommends \  
clang \  
curl \  
g++ \  
gcc \  
git \  
libffi-dev \  
libjpeg-dev \  
libpq-dev \  
libxml2-dev \  
libxslt-dev \  
libyaml-dev \  
llvm-3.5 \  
bzip2 \  
  
# Extra dev tooling  
make \  
vim-nox \  
less \  
ntp \  
&& rm -rf /var/lib/apt/lists/*  
  
# Sane defaults for pip  
ENV PIP_NO_CACHE_DIR off  
ENV PIP_DISABLE_PIP_VERSION_CHECK on  
ENV PYTHONUNBUFFERED 1  
ENV NODE_VERSION 4.4.5  
RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-
linux-x64.tar.gz" \  
&& curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \  
&& grep " node-v$NODE_VERSION-linux-x64.tar.gz\$" SHASUMS256.txt.asc |
sha256sum -c - \  
&& tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local \--strip-
components=1 \  
&& rm "node-v$NODE_VERSION-linux-x64.tar.gz" SHASUMS256.txt.asc  
  
# make the "en_US.UTF-8" locale so postgres will be utf-8 enabled by default  
RUN apt-get update && apt-get install -y locales && rm -rf
/var/lib/apt/lists/* \  
&& localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias
en_US.UTF-8  
ENV LANG en_US.utf8  
  
  
ENV PG_MAJOR 9.5  
ENV PG_VERSION 9.5.*  
ENV PATH /usr/lib/postgresql/$PG_MAJOR/bin:$PATH  
  
RUN apt-key update  
  
RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main'
$PG_MAJOR > /etc/apt/sources.list.d/pgdg.list \  
&& apt-get update && apt-get install -y --force-yes --no-install-recommends \  
postgresql-common \  
postgresql-$PG_MAJOR=$PG_VERSION \  
postgresql-client-$PG_MAJOR=$PG_VERSION \  
postgresql-contrib-$PG_MAJOR=$PG_VERSION \  
&& rm -rf /var/lib/apt/lists/* \  
&& rm "/etc/postgresql/$PG_MAJOR/main/pg_hba.conf" \  
&& touch "/etc/postgresql/$PG_MAJOR/main/pg_hba.conf" \  
&& chown -R postgres "/etc/postgresql/$PG_MAJOR/main/pg_hba.conf" \  
&& { echo; echo "host all all 0.0.0.0/0 trust"; } >>
"/etc/postgresql/$PG_MAJOR/main/pg_hba.conf" \  
&& { echo; echo "local all all trust"; } >>
"/etc/postgresql/$PG_MAJOR/main/pg_hba.conf"  
  
RUN service postgresql start \  
&& createdb -U postgres -E utf-8 --template template0 sentry \  
&& service postgresql stop  
  
ENV DEBIAN_FRONTEND=noninteractive  
RUN apt-get update && apt-get install -y --no-install-recommends \  
redis-server \  
memcached \  
postfix \  
&& rm -rf /var/lib/apt/lists/*  
  
RUN mkdir -p /usr/src/sentry  
ADD ./ /usr/src/sentry/  
  
RUN mkdir -p /etc/sentry  
WORKDIR /usr/src/sentry  
  
ENV SENTRY_CONF /etc/sentry  
ENV C_FORCE_ROOT 1  
ADD scripts/docker-entrypoint.sh /entrypoint.sh  
ENTRYPOINT [ "/entrypoint.sh" ]  
  
EXPOSE 8000  
CMD [ "bash" ]  

