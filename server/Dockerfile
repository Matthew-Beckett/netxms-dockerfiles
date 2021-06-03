# Dockerfile for building NetXMS server image

FROM debian:buster-slim
MAINTAINER Matt Beckett <matt@beckett.cloud>
ENV MAJOR_VERSION=3.8 MINOR_VERSION=382
ENV S6_OVERLAY_VERSION=v2.2.0.1 S6_LOGGING=0
ENV NETXMS_UNLOCKONSTARTUP=1 NETXMS_STARTAGENT=1 NXAGENT_REGISTERSERVER=127.0.0.1

VOLUME /data
EXPOSE 4701

ADD https://github.com/just-containers/s6-overlay/releases/download/${S6_OVERLAY_VERSION}/s6-overlay-amd64-installer /tmp/
RUN chmod +x /tmp/s6-overlay-amd64-installer && /tmp/s6-overlay-amd64-installer /

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && apt-get -y install curl apt-transport-https gnupg && \
    curl -sL http://packages.netxms.org/netxms.gpg | apt-key add - && \
    echo "deb http://packages.netxms.org/debian/ buster main" > /etc/apt/sources.list.d/netxms.list && \
    apt-get update && apt-get -y install netxms-base="${MAJOR_VERSION}.${MINOR_VERSION}-1" \ 
    netxms-server="${MAJOR_VERSION}.${MINOR_VERSION}-1" \
    netxms-agent="${MAJOR_VERSION}.${MINOR_VERSION}-1" \
    netxms-dbdrv-sqlite3="${MAJOR_VERSION}.${MINOR_VERSION}-1" \
    netxms-dbdrv-pgsql="${MAJOR_VERSION}.${MINOR_VERSION}-1" \
    netxms-dbdrv-mariadb="${MAJOR_VERSION}.${MINOR_VERSION}-1" \
    openssl \
    && apt-get clean

COPY server/etc /etc
COPY server/opt /opt

ENTRYPOINT ["/init"]