FROM ubuntu:14.04
MAINTAINER Vinish Soman <vinish86@gmail.com>
# Install packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -y

RUN apt-get -y install apache2 libapache2-mod-jk
RUN apt-get -y install vim wget curl

RUN printf '%s\n' /DocumentRoot/a 'JkMount /* ajp13_worker' . w q | ex -s /etc/apache2/sites-enabled/000-default.conf
RUN sed -i -e"s/^worker.ajp13_worker.host\s*=\s*localhost/worker.ajp13_worker.host=10.5.1.170/" /etc/libapache2-mod-jk/workers.properties

EXPOSE 80

CMD /usr/sbin/apache2ctl -D FOREGROUND

