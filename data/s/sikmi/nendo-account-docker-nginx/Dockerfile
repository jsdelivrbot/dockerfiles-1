FROM nginx:1-alpine  
COPY config/nginx.conf /etc/nginx/nginx.conf  
RUN rm -v /etc/nginx/conf.d/default.conf  
COPY config/conf.d/nendo-account.conf /etc/nginx/conf.d/nendo-account.conf  

