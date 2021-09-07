# Dockerfile for building NetXMS webui

FROM tomcat:10.1-jdk11-openjdk-slim-buster
LABEL org.opencontainers.image.source https://github.com/Matthew-Beckett/netxms-dockerfiles

ENV MAJOR_VERSION=3.9 MINOR_VERSION=229 NETXMS_SERVER=127.0.0.1 NETXMS_SESSIONTIMEOUT=120 NETXMS_ENABLEADVANCEDSETTINGS=true

COPY webui/docker-entrypoint.sh /

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && apt-get -y install wget apt-transport-https && \
    wget -O /usr/local/tomcat/webapps/nxmc.war http://www.netxms.org/download/releases/${MAJOR_VERSION}/nxmc-${MAJOR_VERSION}.${MINOR_VERSION}.war && \
    sha256sum /usr/local/tomcat/webapps/nxmc.war && \
    chmod 755 /docker-entrypoint.sh

ENTRYPOINT [ "/docker-entrypoint.sh" ]
