FROM mhart/alpine-node:6.9.4  
ADD . .  
  
# If you have native dependencies, you'll need extra tools  
# RUN apk add --no-cache make gcc g++ python  
# If you need npm, don't use a base tag  
RUN npm install  
  
EXPOSE 4000  
CMD ["node", "app.js"]

