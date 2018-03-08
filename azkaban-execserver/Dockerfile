FROM ubuntu:16.04

ENV \
    MYSQL_JDBC_VERSION=5.1.45 \
    AZKABAN_VERSION=3.44.0

RUN apt update -y 
RUN apt upgrade -y
RUN apt install default-jdk mysql-client ca-certificates curl git unzip netcat -y

RUN git clone https://github.com/azkaban/azkaban.git && cd azkaban \
    && git checkout tags/$AZKABAN_VERSION \
    && ./gradlew distZip

RUN unzip /azkaban/build/distributions/azkaban-exec-server-${AZKABAN_VERSION}.zip -d /opt \
    && ln -s /opt/azkaban-exec-server-${AZKABAN_VERSION} /opt/azkaban-exec-server \
    && mkdir -p /opt/azkaban-exec-server-${AZKABAN_VERSION}/conf /opt/azkaban-exec-server-${AZKABAN_VERSION}/extlib \
    && curl -sLk http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-$MYSQL_JDBC_VERSION.tar.gz | tar xz

RUN rm -rf /opt/azkaban-exec-server/conf/*

# Install s6-overlay
ADD https://github.com/just-containers/s6-overlay/releases/download/v$S6_OVERLAY_VERSION/s6-overlay-amd64.tar.gz /tmp/
RUN tar xzf /tmp/s6-overlay-amd64.tar.gz -C /

    # Clean
RUN apt-get remove -y --purge \
           $BUILD_DEPS \
    && apt-get autoremove -y --purge \
    && find . -type d -name ".git" | xargs rm -rf \
    && rm -rf \
           /tmp/* \
           /usr/local/lib/* \
           /var/lib/apt/lists/* \
           /var/www/.git \
           /var/tmp/* \
           /usr/share/man \
           /usr/share/doc \
           /usr/share/doc-base \
           /var/www/html

COPY ./root/etc /etc/
COPY ./root/azkaban.properties /root/azkaban.properties

EXPOSE 12321

WORKDIR /opt/azkaban-exec-server-${AZKABAN_VERSION}

ENTRYPOINT [ "/init" ]
