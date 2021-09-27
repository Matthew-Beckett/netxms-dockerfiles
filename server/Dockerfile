# Dockerfile for building NetXMS server image

FROM debian:buster-slim
LABEL org.opencontainers.image.source https://github.com/Matthew-Beckett/netxms-dockerfiles
ENV MAJOR_VERSION=3.9 MINOR_VERSION=280
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
    netxms-dbdrv-sqlite3="${MAJOR_VERSION}.${MINOR_VERSION}-1" \
    netxms-dbdrv-pgsql="${MAJOR_VERSION}.${MINOR_VERSION}-1" \
    netxms-dbdrv-mariadb="${MAJOR_VERSION}.${MINOR_VERSION}-1" \
    openssl \
    && apt-get clean

COPY server/etc /etc
COPY server/opt /opt

COPY server/usr/share/netxms/mibs /usr/share/netxms/mibs
RUN nxmibc -d /usr/share/netxms/mibs -o /usr/share/netxms/mibs/netxms.mib

ENTRYPOINT ["/init"]