FROM terragontech/node:6.9  
RUN mkdir -p /usr/src/app  
WORKDIR /usr/src/app  
COPY package.json /usr/src/app/  
COPY package-lock.json /usr/src/app/  
RUN npm install && npm cache clean  
COPY . /usr/src/app  
EXPOSE 9085  
CMD ["npm","start"]

