FROM ubuntu:14.04
MAINTAINER Vinish Soman <vinish86@gmail.com>
# Install packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -y
RUN apt-get -y install vim wget curl

RUN wget -O /opt/tomcat8.tar.gz http://mirror.olnevhost.net/pub/apache/tomcat/tomcat-8/v8.0.15/bin/apache-tomcat-8.0.15.tar.gz
RUN wget -O /opt/jdk8.tar.gz --no-check-certificate -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-linux-x64.tar.gz


RUN mkdir /opt/tomcat8
RUN mkdir /opt/jdk8

WORKDIR /opt/tomcat8/
RUN tar -zxvf /opt/tomcat8.tar.gz --strip-components=1 -C .
WORKDIR /opt/jdk8
RUN tar -zxvf /opt/jdk8.tar.gz --strip-components=1 -C .

#JAVA_HOME
ENV JAVA_HOME /opt/jdk8
ENV PATH $JAVA_HOME/bin:$PATH

#TOMCAT_HOME
ENV CATALINA_HOME /opt/tomcat8
ENV PATH $PATH:$CATALINA_HOME/bin

#Enable TOMCAT Management GUI username:tomcat and password:tomcat
RUN sed '$i<user username="tomcat" password="tomcat" roles="tomcat,admin,admin-gui,manager,manager-gui"/>' /opt/tomcat8/conf/tomcat-users.xml > /opt/tomcat8/conf/tomcat-users.xml-1
RUN rm -rf /opt/tomcat8/conf/tomcat-users.xml
RUN mv /opt/tomcat8/conf/tomcat-users.xml-1 /opt/tomcat8/conf/tomcat-users.xml

#Start Tomcat in the foreground
CMD ["/opt/tomcat8/bin/catalina.sh", "run"]


EXPOSE 8080 
EXPOSE 8009
 
