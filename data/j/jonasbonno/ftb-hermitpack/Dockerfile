FROM java:8-jre  
  
MAINTAINER Jonas Bonno Mikkelsen (https://github.com/JonasBonno)  
  
# Updating container  
RUN apt-get update && \  
apt-get upgrade --yes --force-yes && \  
apt-get clean && \  
rm -rf /var/lib/apt/lists/*  
  
# Setting workdir  
WORKDIR /minecraft  
  
# Changing user to root  
USER root  
  
# Creating user and downloading files  
RUN useradd -m -U minecraft && \  
mkdir -p /minecraft/world && \  
wget --no-check-certificate https://addons-
origin.cursecdn.com/files/2393/958/FTBPresentsHermitPackServer_1.7.0.zip -O
FTBPresentsHermitPackServer.zip && \  
unzip FTBPresentsHermitPackServer.zip && \  
rm FTBPresentsHermitPackServer.zip && \  
chmod u+x FTBInstall.sh ServerStart.sh && \  
echo "#By changing the setting below to TRUE you are indicating your agreement
to our EULA (https://account.mojang.com/documents/minecraft_eula)." > eula.txt
&& \  
echo "$(date)" >> eula.txt && \  
echo "eula=TRUE" >> eula.txt && \  
chown -R minecraft:minecraft /minecraft  
USER minecraft  
  
# Running install  
RUN /minecraft/FTBInstall.sh  
  
# Expose port 25565  
EXPOSE 25565  
# Expose volume  
VOLUME ["/minecraft/world"]  
  
# Start server  
CMD ["/bin/bash", "/minecraft/ServerStart.sh"]  

