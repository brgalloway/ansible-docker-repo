FROM centos:latest

# Configure the container for SSH
RUN yum -y update --setopt=tsflags=nodocs \
    && yum -y install bind bind-utils \
    && yum -y install openssh-server openssh \
    && yum -y install iproute

# Configure ssh for acess
RUN echo 'root:password' | chpasswd

RUN ssh-keygen -q -b 1024 -N '' -t rsa -f /etc/ssh/ssh_host_rsa_key  \
    && ssh-keygen -q -b 1024 -N '' -t dsa -f /etc/ssh/ssh_host_dsa_key  \
    && ssh-keygen -q -b 521 -N '' -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key  \
    && sed -i -r 's/.?UseDNS\syes/UseDNS no/' /etc/ssh/sshd_config  \
    && sed -i -r 's/.?ChallengeResponseAuthentication.+/ChallengeResponseAuthentication no/' /etc/ssh/sshd_config  \
    && sed -i -r 's/.?PermitRootLogin.+/PermitRootLogin yes/' /etc/ssh/sshd_config 

# Installing bind and installing the correct files
ADD named.conf /etc
RUN mkdir -p /var/named/slaves
RUN touch /var/named/slaves/locust.ulcert.uw.edu.txt

EXPOSE 22 53
EXPOSE 53/udp

CMD ["/usr/sbin/sshd", "-D"]
