FROM alexellis2/node4.x-arm:latest  
  
USER root  
WORKDIR /var/www/  
RUN mkdir -p ghost  
RUN apt-get update && apt-get -qy install wget unzip && \  
wget https://ghost.org/zip/ghost-0.8.0.zip && \  
unzip ghost-*.zip -d ghost && \  
apt-get -y remove wget unzip && \  
rm -rf /var/lib/apt/lists/*  
  
RUN useradd ghost -m -G www-data -s /bin/bash  
RUN chown ghost:www-data .  
RUN chown ghost:www-data ghost  
RUN chown ghost:www-data -R ghost/*  
RUN npm install -g pm2  
  
USER ghost  
WORKDIR /var/www/ghost  
RUN /bin/bash -c "time (npm install sqlite3)"  
RUN npm install  
  
EXPOSE 2368  
EXPOSE 2369  
RUN ls && pwd  
  
ENV NODE_ENV production  
  
RUN sed -e s/127.0.0.1/0.0.0.0/g ./config.example.js > ./config.js  
CMD ["pm2", "start", "index.js", "--name", "blog", "--no-daemon"]

