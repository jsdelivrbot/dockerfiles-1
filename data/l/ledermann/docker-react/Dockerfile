# Build with Node.JS  
FROM node:alpine as build-stage  
WORKDIR /app  
COPY package*.json ./  
RUN yarn install  
COPY . .  
RUN yarn build  
RUN CI="true" yarn test  
  
# Production with Nginx  
FROM nginx:stable-alpine  
COPY nginx.conf /etc/nginx/conf.d/default.conf  
COPY \--from=build-stage /app/build /usr/share/nginx/html  

