#
------------------------------------------------------------------------------  
# Copyright 2018 Frank V. Castellucci and Arthur Greef  
#  
# Licensed under the Apache License, Version 2.0 (the "License");  
# you may not use this file except in compliance with the License.  
# You may obtain a copy of the License at  
#  
# http://www.apache.org/licenses/LICENSE-2.0  
#  
# Unless required by applicable law or agreed to in writing, software  
# distributed under the License is distributed on an "AS IS" BASIS,  
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  
# See the License for the specific language governing permissions and  
# limitations under the License.  
#
-----------------------------------------------------------------------------  
# This docker file creates the development hashblock-dev-rest image  
FROM ubuntu:xenial as base  
LABEL maintainers="Frank V. Castellucci, Arthur Greef"  
  
RUN apt-get update && \  
apt-get install -y -q \  
apt-transport-https \  
python3-dev \  
python3-pip  
  
RUN mkdir -p /builder && \  
pip3 install \  
grpcio-tools \  
grpcio && \  
rm -rf /var/lib/apt/lists/  
  
WORKDIR /builder  
  
COPY bin bin  
COPY libs libs  
COPY apps apps  
COPY protos protos  
COPY families families  
  
RUN bin/protogen && \  
pip3 uninstall -y grpcio grpcio-tools  
  
# The final image  
FROM ubuntu:xenial  
LABEL maintainers="Frank V. Castellucci, Arthur Greef"  
  
RUN apt-get update \  
&& apt-get install -y -q \  
apt-transport-https \  
libssl-dev \  
libffi-dev \  
python3-dev \  
python3-pip  
  
RUN pip3 install --upgrade pip setuptools && \  
# pip3 install wheel && \  
rm -r /root/.cache  
  
RUN pip3 install cryptography --no-binary cryptography  
  
RUN pip3 install sawtooth-sdk --upgrade && \  
mkdir -p /project/hashblock-exchange && \  
mkdir -p /project/hashblock-exchange/apps && \  
mkdir -p /project/hashblock-exchange/bin && \  
mkdir -p /project/hashblock-exchange/modules  
  
WORKDIR /project/hashblock-exchange  
RUN touch __init__.py  
COPY modules modules  
COPY \--from=base /builder/libs/hbzksnark /project/hashblock-
exchange/bin/hbzksnark  
COPY apps/shared apps/shared  
COPY \--from=base /builder/apps/protobuf apps/protobuf  
COPY apps/hashblock_rest apps/hashblock_rest  
  
RUN pip3 install --trusted-host pypi.python.org -r
apps/hashblock_rest/requirements.txt  
  
ENV PYTHONPATH /project/hashblock-
exchange/apps/hashblock_rest:/project/hashblock-
exchange/apps:/project/hashblock-exchange  
  
ENV PATH $PATH:/project/hashblock-exchange/bin:/project/hashblock-
exchange/libs  
  
CMD gunicorn -b 0.0.0.0:8000 --access-logfile -
"hashblock_rest.app:application"  

