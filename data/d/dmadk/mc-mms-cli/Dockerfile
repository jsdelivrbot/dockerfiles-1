FROM java:8  
RUN mkdir -p /data  
RUN wget --progress=bar
"https://dma.ci.cloudbees.com/job/MaritimeCloudSandbox/lastSuccessfulBuild/artifact/mc-
mms-cli/target/*zip*/target.zip" -O /archive.zip && unzip /archive.zip -d / &&
rm -rf /archive.zip  
ADD ./start.sh /start.sh  
ENV ARGUMENTS -help  
CMD ["/bin/bash", "/start.sh"]  

