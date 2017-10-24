FROM centos
RUN yum -y install rsyslog
COPY rsyslog.conf /etc/rsyslog.conf
CMD ["rsyslogd", "-n"]
