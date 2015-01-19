FROM debian
MAINTAINER mlagneaux

RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup | bash -
RUN apt-get install -y nodejs

CMD /bin/bash
