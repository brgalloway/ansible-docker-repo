FROM ubuntu:16.04

# Configure the container for SSH
RUN apt-get update \
    && apt-get install -y python-simplejson \
    && apt-get install -y openssh-server 
RUN mkdir -p /var/run/sshd
RUN echo 'root:password' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

# Installing bind and installing the correct files
RUN apt-get install -y bind9 bind9utils bind9-doc
RUN echo " " > /etc/named.conf

ADD named.conf /etc/
RUN mkdir -p /var/named/slaves
RUN touch /var/named/slaves/locust.ulcert.uw.edu.txt

EXPOSE 22 53
CMD ["/usr/sbin/sshd", "-D"]
