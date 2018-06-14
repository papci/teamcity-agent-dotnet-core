FROM jetbrains/teamcity-agent
FROM ubuntu:18.04
LABEL maintainer "P-A <pa@nextinpact.com>"

#installing wget
RUN apt-get update -y
RUN apt-cache search wget 
RUN apt-get install wget -y
#installing gpg
RUN apt-get install gpg -y
# install .NET Core
RUN wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg
RUN mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
RUN wget -q https://packages.microsoft.com/config/ubuntu/18.04/prod.list 
RUN mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
RUN chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
RUN chown root:root /etc/apt/sources.list.d/microsoft-prod.list

RUN apt-get install apt-transport-https -y
RUN apt-get update

RUN apt-get install tzdata -y 
RUN apt-cache search dotnet-sdk 
# install .NET Core
ENV DOTNET_VER "dotnet-sdk-2.1"
#(apt-cache search dotnet-dev-2.1 | awk '{print $1}') | sh 
RUN apt-get install ${DOTNET_VER} -y

# install mono-devel
RUN apt-get install mono-devel mono-dbg mono-xbuild libmono-addins-* -y 
    
#npm utilities
RUN apt-get install nodejs -y
RUN npm install npm -g
RUN install bower gulp -g

# install ansible
RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 && \
    apt-get update && \
    apt-get install -y ansible

VOLUME /opt/buildagent/work
VOLUME /opt/buildagent/logs
VOLUME /data/teamcity_agent/conf
VOLUME /opt/buildagent/plugins

ENV DOCKER_HOST ""
ENV DOCKER_BIN "/usr/bin/docker"
