FROM madnificent/ember:3.0.0 as builder  
  
LABEL maintainer="info@redpencil.io"  
  
WORKDIR /app  
COPY package.json .  
RUN npm install  
COPY . .  
RUN ember build -prod  
  
FROM semtech/ember-proxy-service:1.3.0  
ENV STATIC_FOLDERS_REGEX "^/(assets|font|files)/"  
COPY ./proxy/torii-authorization.conf /config/torii-authorization.conf  
COPY ./proxy/file-upload.conf /config/file-upload.conf  
  
COPY \--from=builder /app/dist /app  

