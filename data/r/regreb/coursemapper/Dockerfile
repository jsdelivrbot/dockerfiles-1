FROM node:6  
WORKDIR /home/node/app  
  
RUN yarn global add nodemon grunt-cli bower gulp npm-run-all  
  
ADD package.json .  
RUN yarn install --silent --non-interactive \--production=false  
ADD . .  
RUN bower install --silent --allow-root && grunt > /dev/null  
  
ENV NODE_ENV=production  
ENV DATABASE=mongodb/course_mapper  
ENV PORT=3000  
EXPOSE 3000  
  
USER node  
CMD ["bin/www"]  

