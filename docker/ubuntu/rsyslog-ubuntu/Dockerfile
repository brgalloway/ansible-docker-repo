FROM ubuntu:xenial

RUN apt-get update && \
    apt-get install -y rsyslog && \
    rm /etc/rsyslog.d/50-default.conf

COPY 10-server.conf /etc/rsyslog.d
COPY rsyslog.conf /etc/rsyslog.conf

EXPOSE 514 514/udp

ENTRYPOINT [ "rsyslogd", "-n"]

