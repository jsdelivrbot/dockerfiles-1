#  
# Licensed to the Apache Software Foundation (ASF) under one or more  
# contributor license agreements. See the NOTICE file distributed with  
# this work for additional information regarding copyright ownership.  
# The ASF licenses this file to You under the Apache License, Version 2.0  
# (the "License"); you may not use this file except in compliance with  
# the License. You may obtain a copy of the License at  
#  
# http://www.apache.org/licenses/LICENSE-2.0  
#  
# Unless required by applicable law or agreed to in writing, software  
# distributed under the License is distributed on an "AS IS" BASIS,  
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  
# See the License for the specific language governing permissions and  
# limitations under the License.  
#  
FROM uscdatascience/tf-tika-base  
MAINTAINER Apache Tika Team  
  
# Download the pretrained im2txt checkpoint  
WORKDIR /usr/share/apache-tika/models/dl/image/caption/  
  
RUN echo "We're downloading the checkpoint file for image captioning, the
shell might look unresponsive. Please be patient." && \  
# To get rid of early EOF error  
git config --global http.postBuffer 1048576000 && \  
git clone https://github.com/USCDataScience/img2text.git && \  
# Join the parts  
cat img2text/models/1M_iters_ckpt_parts_* >1M_iters_ckpt.tar.gz && \  
tar -xzvf 1M_iters_ckpt.tar.gz && rm -rf 1M_iters_ckpt.tar.gz  
  
RUN curl -O https://raw.githubusercontent.com/apache/tika/master/tika-
parsers/src/main/resources/org/apache/tika/parser/captioning/tf/model_info.xml  
  
# Download server related source files  
WORKDIR /usr/share/apache-tika/src/dl/image/caption/  
  
RUN curl -O https://raw.githubusercontent.com/ThejanW/tika/master/tika-
parsers/src/main/resources/org/apache/tika/parser/captioning/tf/caption_generator.py
&& \  
curl -O https://raw.githubusercontent.com/ThejanW/tika/master/tika-
parsers/src/main/resources/org/apache/tika/parser/captioning/tf/im2txtapi.py
&& \  
curl -O https://raw.githubusercontent.com/ThejanW/tika/master/tika-
parsers/src/main/resources/org/apache/tika/parser/captioning/tf/model_wrapper.py
&& \  
curl -O https://raw.githubusercontent.com/ThejanW/tika/master/tika-
parsers/src/main/resources/org/apache/tika/parser/captioning/tf/vocabulary.py
&& \  
chmod +x im2txtapi.py  
  
WORKDIR /  
  
# Remove unnecessary packages comes with base  
RUN apt-get -y remove \  
apt-utils \  
curl \  
git \  
software-properties-common \  
unzip \  
wget  
  
# Add symbolic link to im2txtapi.py  
RUN ln -s /usr/share/apache-tika/src/dl/image/caption/im2txtapi.py
/usr/bin/im2txtapi  
  
# expose API port, this is the default port  
EXPOSE 8764  
CMD im2txtapi  

