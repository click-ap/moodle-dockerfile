FROM moodletw/httpd:5.6-centos7
MAINTAINER Click-AP

ENV Customer=lawbroker

USER root

#Install SVN client from official repository
#RUN echo $'[WandiscoSVN] \n\
#name=Wandisco SVN Repo \n\
#baseurl=http://opensource.wandisco.com/centos/7/svn-1.9/RPMS/$basearch/ \n\
#enabled=1 \n\
#gpgcheck=0 ' > /etc/yum.repos.d/wandisco-svn.repo

#RUN cat /etc/yum.repos.d/wandisco-svn.repo
#RUN yum update -y \
# && yum install -y subversion \

#RUN svn --version
#RUN svn co --non-interactive --no-auth-cache --username --password http://192.168:18080/svn/lawbroker/branches/law2 /vaw/www/html/lawbroker

RUN yum update -y \
 && yum clean all \
 && usermod -aG apache docker 

VOLUME ["/var/moodledata"]

ADD lawbroker /var/www/html/lawbroker

ADD entrypoint /usr/local/entrypoint
RUN chmod -v +x /usr/local/entrypoint \
 && ln -sf /dev/stdout /var/log/httpd/access_log \
 && ln -sf /dev/stderr /var/log/httpd/error_log \
 && mkdir -p /var/moodledata \
 && chown -R docker:apache /var/moodledata/

USER docker

EXPOSE 80
WORKDIR /var/www/html
ENTRYPOINT ["/tini", "--", "/usr/local/entrypoint"]