FROM ubuntu:18.04

#I am the boss here!
MAINTAINER Firat Turker "firat@byfirat.com"
WORKDIR /root/kurento_test

#First, make sure that GnuPG is installed.
RUN apt-get update && apt-get install --no-install-recommends --yes gnupg

#To avoid interactive installation errors
RUN apt-get install apt-utils -y

#Some useful tools willl be need
RUN apt-get install wget -y
RUN apt-get install git -y
RUN apt-get install curl -y

#Import the Kurento repository signing key
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 5AFA7A83

#Get Ubuntu version definitions
RUN  /bin/bash -c "source /etc/upstream-release/lsb-release 2>/dev/null" || /bin/bash -c "source /etc/lsb-release"

#Add the repository to Apt
RUN echo '# Kurento Media Server - Release packages\n\
deb [arch=amd64] http://ubuntu.openvidu.io/6.15.0 bionic kms6\n'\
>> /etc/apt/sources.list.d/kurento.list


RUN apt-get update -y
RUN apt-get install vim nano -y
RUN apt-get install --no-install-recommends --yes kurento-media-server

RUN service kurento-media-server start
RUN service kurento-media-server stop
RUN apt install default-jre -y
RUN apt install default-jdk -y
RUN apt install maven -y
RUN service kurento-media-server start
RUN git clone https://github.com/firatturker/Kurento_demo.git
RUN cd Kurento_demo/kurento-one2many-call &&  mvn clean install 
WORKDIR /root/kurento_test/Kurento_demo/kurento-one2many-call/target
EXPOSE 8888
ENTRYPOINT ["java", "-jar", "kurento-one2many-call-6.15.0-exec.jar"]

#to build: sudo docker build -t kurento_test:1.0 .
#to run: sudo docker run --network host kurento_test:1.0

