FROM java:7-jre
MAINTAINER mlagneaux

RUN	apt-get update
RUN	apt-get install -y wget

WORKDIR /tmp

RUN wget http://mir2.ovh.net/ftp.apache.org/dist/tomcat/tomcat-7/v7.0.57/bin/apache-tomcat-7.0.57.tar.gz

RUN tar -xvf apache-tomcat-7.0.57.tar.gz
RUN cp -R apache-tomcat-7.0.57 /usr/share/tomcat7
RUN mkdir -p /usr/share/tomcat7/shared/classes
RUN mkdir -p /usr/share/tomcat7/shared/lib
RUN sed -i.bak 's/^shared.loader=.*/shared.loader=\${catalina.home}\/shared\/classes,\${catalina.home}\/shared\/lib\/\*.jar/' /usr/share/tomcat7/conf/catalina.properties
RUN touch /usr/share/tomcat7/logs/catalina.out

RUN rm -rf apache-tomcat-7.0.57*

WORKDIR /usr/share/tomcat7

EXPOSE 8080

CMD /usr/share/tomcat7/bin/startup.sh && tail -f /usr/share/tomcat7/logs/catalina.out