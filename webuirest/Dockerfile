# Dockerfile for building NetXMS webui

FROM ghcr.io/matthew-beckett/netxms_webui:3.9.334
LABEL org.opencontainers.image.source https://github.com/Matthew-Beckett/netxms-dockerfiles

ENV MAJOR_VERSION=3.9 MINOR_VERSION=334 NETXMS_SERVER=127.0.0.1 NETXMS_SESSIONTIMEOUT=120 NETXMS_ENABLEADVANCEDSETTINGS=true

COPY webuirest/docker-entrypoint.sh /

RUN wget -O /usr/local/tomcat/webapps/nxapisrv.war http://www.netxms.org/download/releases/${MAJOR_VERSION}/netxms-websvc-${MAJOR_VERSION}.${MINOR_VERSION}.war && \
    sha256sum /usr/local/tomcat/webapps/nxapisrv.war && \
    chmod 755 /docker-entrypoint.sh
    
ENTRYPOINT [ "/docker-entrypoint.sh" ]
