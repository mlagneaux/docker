FROM mlagneaux/java_7_jre-tomcat_7
MAINTAINER mlagneaux <mlagneaux@gmail.com>

#---------------------------#
# Install required packages #
#---------------------------#
RUN	apt-get update
RUN	apt-get install -y unzip
RUN apt-get install -y imagemagick
RUN apt-get install -y libreoffice-impress
RUN apt-get install -y libreoffice-writer
RUN apt-get install -y libreoffice-calc
RUN apt-get install -y postgresql

WORKDIR /tmp

#------------------------#
# Get required resources #
#------------------------#
RUN wget http://dl.alfresco.com/release/community/5.0.c-build-00145/alfresco-community-5.0.c.zip

#------------------#
# Install Alfresco #
#------------------#
RUN unzip alfresco-community-5.0.c.zip

# Install Alfresco webapps
#-------------------------
RUN cp alfresco-community-5.0.c/web-server/webapps/alfresco.war /usr/share/tomcat7/webapps
RUN cp alfresco-community-5.0.c/web-server/webapps/share.war /usr/share/tomcat7/webapps

# Configure Alfresco
#-------------------
RUN cp alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties.sample alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties
RUN sed -i 's/^\#dir.root=.*/dir.root=\/srv\/alfresco\/alf_data/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties
RUN sed -i 's/^\#db.username=/db.username=/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties
RUN sed -i 's/^\#db.password=/db.password=/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties
RUN sed -i 's/^\#db.driver=org.postgresql.Driver/db.driver=org.postgresql.Driver/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties
RUN sed -i 's/^\#db.url=jdbc:postgresql/db.url=jdbc:postgresql/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties
RUN cp alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties /usr/share/tomcat7/shared/classes/alfresco-global.properties

# Install JDBC Driver
#--------------------
RUN cp alfresco-community-5.0.c/web-server/lib/postgresql-9.3-1102-jdbc41.jar /usr/share/tomcat7/shared/lib

#----------------------------#
# Create Alfresco repository #
#----------------------------#
RUN mkdir -p /srv/alfresco/alf_data
RUN /etc/init.d/postgresql start &&\
	su postgres --command "psql -c \"create user alfresco with password 'alfresco'\"" &&\
	su postgres --command "createdb -O alfresco alfresco" &&\
	/etc/init.d/postgresql stop

#-------------------#
# Clean /tmp folder #
#-------------------#
RUN rm -rf alfresco-community-5.0.c*


WORKDIR /usr/share/tomcat7

EXPOSE 8080

CMD /etc/init.d/postgresql start && sleep 10 && /usr/share/tomcat7/bin/startup.sh && tail -f /usr/share/tomcat7/logs/catalina.out