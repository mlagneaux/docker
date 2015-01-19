FROM mlagneaux/java_7_jre-tomcat_7
MAINTAINER mlagneaux

#---------------------------#
# Install required packages #
#---------------------------#
RUN	apt-get update &&\
	apt-get install -y unzip &&\
	apt-get install -y imagemagick &&\
	apt-get install -y libreoffice-impress &&\
	apt-get install -y libreoffice-writer &&\
	apt-get install -y libreoffice-calc &&\
	apt-get install -y postgresql

CMD /bin/bash