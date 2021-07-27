# Dockerfile for building NetXMS server image

FROM debian:buster-slim
LABEL org.opencontainers.image.source https://github.com/Matthew-Beckett/netxms-dockerfiles

ENV MAJOR_VERSION=3.9 MINOR_VERSION=156
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && apt-get -y install curl apt-transport-https gnupg && \
    curl -sL http://packages.netxms.org/netxms.gpg | apt-key add - && \
    echo "deb http://packages.netxms.org/debian/ buster main" > /etc/apt/sources.list.d/netxms.list && \
    apt-get update && apt-get -y install netxms-base="${MAJOR_VERSION}.${MINOR_VERSION}-1" netxms-agent="${MAJOR_VERSION}.${MINOR_VERSION}-1" netxms-dbdrv-sqlite3="${MAJOR_VERSION}.${MINOR_VERSION}-1" && apt-get clean

COPY nxagent/docker-entrypoint.sh /

RUN  chmod 755 /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]
