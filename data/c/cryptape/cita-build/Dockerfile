# usage:  
# git clone http://github.com/cryptape/cita  
# cd cita  
# build with debug  
# docker run -v $PWD:/source cryptape/cita-build  
# build with release  
# docker run -v $PWD:/source cryptape/cita-build bash -c
/source/scripts/config_rabbitmq.sh; make release  
FROM ubuntu:16.04  
ENV PATH $PATH:/root/.cargo/bin  
COPY *.sh /tmp/  
RUN /tmp/install_develop.sh \  
&& rm -rf /var/lib/apt/lists \  
&& rm -rf ~/.cache/pip  
  
WORKDIR /source  
CMD /source/scripts/config_rabbitmq.sh \  
&& make debug  

