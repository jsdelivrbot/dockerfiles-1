# Builds a docker image with the requirements to do kubernetes deploys with
Helm  
FROM google/cloud-sdk  
  
ARG helm_version=2.8.1  
ADD https://storage.googleapis.com/kubernetes-helm/helm-v$helm_version-linux-
amd64.tar.gz /  
  
RUN tar -xzvf /helm-v$helm_version-linux-amd64.tar.gz && \  
mv /linux-amd64/helm /usr/local/bin/ && \  
rm -f /helm-v$helm_version-linux-amd64.tar.gz && \  
helm init -c  

