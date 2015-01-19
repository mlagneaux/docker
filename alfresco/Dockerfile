FROM mlagneaux/alfresco-prerequisites
MAINTAINER mlagneaux <mlagneaux@gmail.com>


WORKDIR /tmp

#--------------------------------#
# Get and Install Alfresco 5.0.c #
#--------------------------------#
RUN wget http://dl.alfresco.com/release/community/5.0.c-build-00145/alfresco-community-5.0.c.zip &&\
	unzip alfresco-community-5.0.c.zip &&\
	cp alfresco-community-5.0.c/web-server/webapps/alfresco.war /usr/share/tomcat7/webapps &&\
	cp alfresco-community-5.0.c/web-server/webapps/share.war /usr/share/tomcat7/webapps &&\
	cp alfresco-community-5.0.c/web-server/lib/postgresql-9.3-1102-jdbc41.jar /usr/share/tomcat7/shared/lib
	
RUN	cp alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties.sample alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties &&\
	sed -i 's/^\#dir.root=.*/dir.root=\/srv\/alfresco\/alf_data/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties &&\
	sed -i 's/^\#db.username=/db.username=/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties &&\
	sed -i 's/^\#db.password=/db.password=/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties &&\
	sed -i 's/^\#db.driver=org.postgresql.Driver/db.driver=org.postgresql.Driver/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties &&\
	sed -i 's/^\#db.url=jdbc:postgresql/db.url=jdbc:postgresql/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties &&\
	sed -i 's/^\#ooo.exe=soffice/ooo.exe=\/usr\/bin\/soffice/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties &&\
	sed -i 's/^\#ooo.enabled=false/ooo.enabled=true/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties &&\
	sed -i 's/^\#jodconverter.enabled=true/jodconverter.enabled=false/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties &&\
	sed -i 's/^\#img.root=.\/ImageMagick/img.root=\/usr/' alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties &&\
	cp alfresco-community-5.0.c/web-server/shared/classes/alfresco-global.properties /usr/share/tomcat7/shared/classes/alfresco-global.properties

#----------------------------#
# Create Alfresco repository #
#----------------------------#
RUN mkdir -p /srv/alfresco/alf_data &&\
	/etc/init.d/postgresql start &&\
	su postgres --command "psql -c \"create user alfresco with password 'alfresco'\"" &&\
	su postgres --command "createdb -O alfresco alfresco" &&\
	/etc/init.d/postgresql stop

#-------------------#
# Clean /tmp folder #
#-------------------#
RUN rm -rf alfresco-community-5.0.c*


WORKDIR /usr/share/tomcat7

EXPOSE 8080

CMD /etc/init.d/postgresql start && sleep 5 && /usr/share/tomcat7/bin/startup.sh && tail -f /usr/share/tomcat7/logs/catalina.out