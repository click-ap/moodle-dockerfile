FROM moodletw/httpd:5.6-centos7
MAINTAINER Click-AP

ENV Customer=lawbroker

USER root

RUN yum update -y \
 && yum clean all \
 && usermod -aG apache docker 

VOLUME ["/var/moodledata"]

ADD trunk /var/www/html

# Simple startup script to avoid some issues observed with container restart
ADD entrypoint /usr/local/entrypoint
RUN chmod -v +x /usr/local/entrypoint \
 && ln -sf /dev/stdout /var/log/httpd/access_log \
 && ln -sf /dev/stderr /var/log/httpd/error_log \
 && mkdir -p /var/moodledata \
 && chown -R docker:apache /var/moodledata/

#USER docker

EXPOSE 80
WORKDIR /var/www/html
ENTRYPOINT ["/tini", "--", "/usr/local/entrypoint"]
#CMD /usr/sbin/apachectl -D FOREGROUND
