FROM fedora:27  
LABEL maintainer="sean@sean.io"  
  
RUN dnf -y install passwd curl emacs-nox gnupg2 initscripts iptables iputils
lsof nc net-tools nmap openssl procps strace systemd-sysv tcpdump telnet vim-
minimal wget which ca-certificates  
  
CMD [ "/usr/lib/systemd/systemd" ]  

