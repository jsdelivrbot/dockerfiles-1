#  
# Minimal image for mkdocs and utilities to create a pdf from  
# the content generated by mkdocs.  
#  
FROM python:slim  
  
ENV PANDOC_VERSION "1.19.2.1"  
ENV DOWNLOAD_URL
"http://github.com/jgm/pandoc/releases/download/$PANDOC_VERSION/pandoc-$PANDOC_VERSION-1-amd64.deb"  
RUN apt-get update && apt-get install -qy wget texlive-xetex git imagemagick  
  
RUN wget $DOWNLOAD_URL -O pandoc.deb && \  
dpkg -i pandoc.deb && rm pandoc.deb  
  
RUN pip install mkdocs && \  
pip install git+https://github.com/backfighter/mkdocs-combine.git && \  
pip install git+https://github.com/facelessuser/pymdown-extensions.git  
# Git is not needed we reduce the size a little bit  
RUN apt-get remove -qy wget git && apt-get clean  

