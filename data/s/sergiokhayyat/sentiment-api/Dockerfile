FROM python:3-alpine  
  
# Install requirements first  
COPY requirements.txt /tmp  
RUN pip install -r /tmp/requirements.txt  
  
# Copy the app  
COPY . /usr/src/app  
WORKDIR /usr/src/app  
  
# Run the app  
EXPOSE 80  
CMD [ "python" , "app.py" ]  

