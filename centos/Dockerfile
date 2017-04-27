


FROM centos:latest

ENV container docker

RUN yum install -y yum-utils \
    && yum-config-manager \
    --add-repo https://download.docker.com/linux/centos/docker-ce.repo \
    && yum makecache fast \
    && yum -y install docker-ce \
    && systemctl start docker

RUN ln -sf /dev/stdout /var/log/messages

EXPOSE 80 443 22

CMD ["/bin/bash/"]
