# Docker image for behave and other Python-based SBE/BDD tools.  
#  
# References:  
# - https://eshlox.net/2016/11/22/dockerize-behave-selenium-tests/  
# - https://gist.github.com/ziadoz/3e8ab7e944d02fe872c3454d17af31a5  
# - https://github.com/SeleniumHQ/docker-selenium  
#  
# pull base image  
FROM python:3.6-slim-stretch  
  
MAINTAINER Xolani Mxoxozi <xolanimxoxozi@gmail.com>  
  
ENV CHROME_DRIVER_VERSION 2.37  
ENV CHROME_DRIVER_TARBALL
http://chromedriver.storage.googleapis.com/$CHROME_DRIVER_VERSION/chromedriver_linux64.zip  
ENV CAPYBARA_PATCH_SRC https://raw.githubusercontent.com/William-
Yeh/capybara.py/master/capybara/selenium/browser.py  
ENV CAPYBARA_PATCH_DEST /usr/local/lib/python3.6/site-
packages/capybara/selenium/browser.py  
  
RUN \  
echo "==> Install common stuff missing from the slim base image..." && \  
apt-get update && \  
apt-get install -y --no-install-recommends \  
gnupg \  
dirmngr \  
wget \  
ca-certificates && \  
rm -rf /var/lib/apt/lists/* && \  
\  
\  
echo "==> Add Google repo for Chrome..." && \  
wget -q -O- https://dl.google.com/linux/linux_signing_key.pub | apt-key add -
&& \  
echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" |
tee /etc/apt/sources.list.d/google.list && \  
\  
\  
echo "==> Install prerequisite stuff..." && \  
apt-get update && \  
apt-get install -y --no-install-recommends \  
python3-dev \  
python3-pip \  
xvfb \  
libfontconfig \  
libfreetype6 \  
xfonts-scalable \  
fonts-liberation \  
fonts-noto-cjk \  
google-chrome-stable && \  
\  
\  
echo "==> Install ChromeDriver..." && \  
wget -qO- $CHROME_DRIVER_TARBALL | zcat > /usr/local/bin/chromedriver && \  
chown root:root /usr/local/bin/chromedriver && \  
chmod 0755 /usr/local/bin/chromedriver && \  
\  
\  
\  
echo "==> Install useful Python stuff..." && \  
pip3 install --no-cache-dir \  
requests \  
unittest-xml-reporting \  
nose \  
mockito \  
pyshould \  
&& \  
\  
\  
echo "==> Install behave and related stuff..." && \  
pip3 install --no-cache-dir \  
behave \  
selenium \  
elementium \  
capybara-py \  
xvfbwrapper && \  
\  
\  
echo "==> Patch Capybara..." && \  
wget -q -O $CAPYBARA_PATCH_DEST $CAPYBARA_PATCH_SRC && \  
\  
\  
echo "==> Clean up..." && \  
rm -rf /var/lib/apt/lists/*  
  
ENV PATH /usr/lib/chromium/:$PATH  

