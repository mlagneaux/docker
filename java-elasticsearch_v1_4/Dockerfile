FROM java
MAINTAINER mlagneaux

RUN apt-get install -y software-properties-common
RUN wget -qO - https://packages.elasticsearch.org/GPG-KEY-elasticsearch | apt-key add -
RUN add-apt-repository "deb http://packages.elasticsearch.org/elasticsearch/1.4/debian stable main"
RUN apt-get update
RUN apt-get install -y elasticsearch
RUN touch /var/log/elasticsearch/elasticsearch.log

EXPOSE 9200

CMD /etc/init.d/elasticsearch start && tail -f /var/log/elasticsearch/elasticsearch.log