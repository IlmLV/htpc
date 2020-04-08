FROM linuxserver/ffmpeg

RUN apt-get update && \
    apt-get install -y openjdk-8-jdk-headless curl tar dcraw && \
    apt-get autoremove && \
    apt-get clean

ENV SERVIIO_VERSION 2.0

RUN DIR=$(mktemp -d) && cd ${DIR} && \
    curl -Os http://download.serviio.org/releases/serviio-${SERVIIO_VERSION}-linux.tar.gz && \
    tar zxvf serviio-${SERVIIO_VERSION}-linux.tar.gz && \
    mv serviio-${SERVIIO_VERSION} /opt/serviio && \
    rm -rf ${DIR}

VOLUME [ "/opt/serviio/config", "/opt/serviio/library",  "/opt/serviio/log", "/opt/serviio/plugins"]

EXPOSE 1900/udp
EXPOSE 8895/tcp
# HTTP/1.1 /console /rest
EXPOSE 23423/tcp 
# HTTPS/1.1 /console /rest
EXPOSE 23523/tcp
# HTTP/1.1 /cds /mediabrowser
EXPOSE 23424/tcp
# HTTPS/1.1 /cds /mediabrowser
EXPOSE 23524/tcp

WORKDIR /opt/serviio
ENTRYPOINT ["bin/serviio.sh"]