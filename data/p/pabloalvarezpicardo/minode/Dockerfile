# Imagen base  
FROM node:latest  
  
# Directorio de la app  
WORKDIR /app  
  
# Copiar los archivos  
ADD . /app  
  
# Dependencias  
RUN npm install  
RUN apt-get update  
RUN apt-get install -y vim  
  
# Puerto  
EXPOSE 3000  
# Comandos  
CMD ["npm", "start"]  

