# Do not edit this file manually, it was generated on 2017-03-10 at 21:52 from
slavepython/Dockerfile.in  
# Define an image for CoolProp Python buildslaves  
FROM coolprop/slavebase32:latest  
# File Author / Maintainer  
MAINTAINER Jorrit Wronski <jowr@ipu.dk>  
# Make sure the follwoing commands are run as root user  
USER root  
WORKDIR /root  
# Install system tools for compilation of Python extensions numpy-scipy-pandas  
RUN apt-key update -qq && apt-get update -qq &&
DEBIAN_FRONTEND="noninteractive" apt-get install -y \  
build-essential gcc python-dev libhdf5-serial-dev libnetcdf-dev liblapack-dev
libatlas-dev libblas-dev && \  
DEBIAN_FRONTEND="noninteractive" apt-get autoclean &&
DEBIAN_FRONTEND="noninteractive" apt-get clean &&
DEBIAN_FRONTEND="noninteractive" apt-get autoremove  
# Make sure the following commands are run as the buildbot user  
USER buildbot  
WORKDIR /home/buildbot  
# Install miniconda Python distribution  
RUN curl -o miniconda.sh
"https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86.sh" && chmod
+x miniconda.sh && linux32 ./miniconda.sh -b && rm miniconda.sh && echo
"export
PATH=/home/buildbot/miniconda3/bin:/home/buildbot/miniconda2/bin:$PATH" >>
/home/buildbot/.bash_profile  
ENV PATH /home/buildbot/miniconda3/bin:/home/buildbot/miniconda2/bin:$PATH  
# Add the miniconda environments for the Python builds  
RUN linux32 conda install conda-build && linux32 conda create -n CoolProp27
python=2.7 cython pip requests jinja2 pyyaml pycrypto numpy scipy matplotlib
pandas wheel && linux32 conda create -n CoolProp33 python=3.3 cython pip
requests jinja2 pyyaml pycrypto numpy scipy matplotlib pandas wheel && linux32
conda create -n CoolProp34 python=3.4 cython pip requests jinja2 pyyaml
pycrypto numpy scipy matplotlib pandas wheel && linux32 conda create -n
CoolProp35 python=3.5 cython pip requests jinja2 pyyaml pycrypto numpy scipy
matplotlib pandas wheel && linux32 conda create -n CoolProp36 python=3.6
cython pip requests jinja2 pyyaml pycrypto numpy scipy matplotlib pandas wheel
&& linux32 conda clean -yilts  

