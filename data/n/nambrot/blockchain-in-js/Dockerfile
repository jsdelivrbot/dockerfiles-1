FROM node:6.9.1  
RUN npm install -g yarn  
  
COPY package.json yarn.lock ./  
RUN yarn --pure-lockfile  
  
COPY ./ ./  
CMD node src/server.js  

