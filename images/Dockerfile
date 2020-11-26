FROM ubuntu:latest
MAINTAINER Zeynalov_Zaka

WORKDIR /usr/apps/hello-docker

RUN apt-get -y update

RUN apt-get install -y nodejs

RUN apt-get install -y npm


RUN npm install -g http-server 

ADD . /usr/apps/hello-docker/

#Portun acislihi!

EXPOSE 80

CMD ["http-server", "-s"]
