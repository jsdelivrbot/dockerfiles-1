# Usage: docker run --restart=always -v /var/data/blockchain-
xmr:/root/.bitmonero -p 18080:18080 -p 18081:18081 --name=monerod -td
kannix/monero-full-node  
FROM ubuntu:16.04  
ENV MONERO_VERSION=0.12.2.0
MONERO_SHA256=cb97e3f8b700a81e1b0f1a77509eefbfb415aa6013f23685f8933b559309c580  
  
RUN apt-get update && apt-get install -y curl bzip2 libpcsclite-dev  
  
# RUN useradd -ms /bin/bash monero  
# USER monero  
# WORKDIR /home/monero  
WORKDIR /root  
  
RUN curl https://downloads.getmonero.org/cli/monero-
linux-x64-v$MONERO_VERSION.tar.bz2 -O &&\  
echo "$MONERO_SHA256 monero-linux-x64-v$MONERO_VERSION.tar.bz2" | sha256sum -c
- &&\  
tar -xjvf monero-linux-x64-v$MONERO_VERSION.tar.bz2 &&\  
rm monero-linux-x64-v$MONERO_VERSION.tar.bz2 &&\  
cp ./monero-v$MONERO_VERSION/monerod . &&\  
rm -r monero-*  
  
# blockchain loaction  
VOLUME /root/.bitmonero  
  
EXPOSE 18080 18081  
ENTRYPOINT ["./monerod"]  
CMD ["--restricted-rpc", "--rpc-bind-ip=0.0.0.0", "--confirm-external-bind"]  

