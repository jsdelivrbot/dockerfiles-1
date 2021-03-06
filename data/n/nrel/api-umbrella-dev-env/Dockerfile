FROM ubuntu:16.04  
RUN mkdir /app  
RUN mkdir /build  
WORKDIR /build  
ENV DOCKER_DEV true  
ENV NOKOGIRI_USE_SYSTEM_LIBRARIES 1  
COPY build/scripts/install_build_dependencies
/app/build/scripts/install_build_dependencies  
COPY build/package_dependencies.sh /app/build/package_dependencies.sh  
RUN env INSTALL_TEST_DEPENDENCIES=true
/app/build/scripts/install_build_dependencies  
  
COPY build/scripts/download_cmake /app/build/scripts/download_cmake  
RUN /app/build/scripts/download_cmake  
  
COPY CMakeLists.txt /app/CMakeLists.txt  
COPY build/cmake/functions /app/build/cmake/functions  
COPY build/cmake/deps /app/build/cmake/deps  
COPY build/cmake/deps.cmake /app/build/cmake/deps.cmake  
COPY build/patches /app/build/patches  
COPY configure /app/configure  
RUN /app/configure && make deps  
  
COPY build/cmake/build-deps /app/build/cmake/build-deps  
COPY build/cmake/build-deps.cmake /app/build/cmake/build-deps.cmake  
RUN /app/configure && make build-deps  
  
COPY build/cmake/test-deps /app/build/cmake/test-deps  
COPY build/cmake/test-deps.cmake /app/build/cmake/test-deps.cmake  
RUN /app/configure && make test-deps  
  
COPY Gemfile /app/Gemfile  
COPY Gemfile.lock /app/Gemfile.lock  
COPY build/cmake/test-bundle.cmake /app/build/cmake/test-bundle.cmake  
RUN /app/configure && make test-bundle  
  
COPY build/cmake/app-deps /app/build/cmake/app-deps  
COPY build/cmake/app-deps.cmake /app/build/cmake/app-deps.cmake  
RUN /app/configure && make app-deps  
  
COPY . /app  
RUN /app/configure && make && \  
rm -rf /build/build/work/src/api-umbrella-core/tmp/admin-ui-
build/node_modules/*/.node_modules.ember-try  
  
RUN groupadd -r api-umbrella && \  
useradd -r -g api-umbrella -s /sbin/nologin -d /opt/api-umbrella -c "API
Umbrella user" api-umbrella  
  
ENV PATH "/app/bin:/build/build/work/dev-env/sbin:/build/build/work/dev-
env/bin:/build/build/work/test-env/sbin:/build/build/work/test-
env/bin:/build/build/work/stage/opt/api-
umbrella/sbin:/build/build/work/stage/opt/api-
umbrella/bin:/build/build/work/stage/opt/api-
umbrella/embedded/sbin:/build/build/work/stage/opt/api-
umbrella/embedded/bin:${PATH}"  
ENV API_UMBRELLA_ROOT /build/build/work/stage/opt/api-umbrella  
  
WORKDIR /app  
  
ENTRYPOINT ["/app/docker/dev/docker-entrypoint"]  
CMD ["/app/docker/dev/docker-start"]  

