FROM consol/omd-labs-centos:nightly  
  
MAINTAINER Simon Meggle "simon.meggle@consol.de"  
ENV REFRESHED_AT 2017-12-18  
ENV TZ Europe/Berlin  
  
# Add the Ansible provisioning role  
ADD ansible_provision /root/ansible_provision  
  
RUN /omd/sites/$SITENAME/bin/ansible-playbook -i localhost,
/root/ansible_provision/playbook.yml -c local -e GRAPHER=pnp4nagios -e
SITENAME=$SITENAME  

