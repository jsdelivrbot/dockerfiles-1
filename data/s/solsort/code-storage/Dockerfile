FROM node:latest  
  
COPY . /usr/src/app  
WORKDIR /usr/src/app  
RUN npm install --production  
ENTRYPOINT ["node", "code-storage.js"]  
EXPOSE 8888  

