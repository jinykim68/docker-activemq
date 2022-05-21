FROM openjdk:11-slim

ENV ACTIVEMQ_VERSION=5.17.1
ENV ACTIVEMQ=apache-activemq-${ACTIVEMQ_VERSION}
ENV ACTIVEMQ_HOME=/opt/activemq

RUN apt-get update && \
    apt-get install -y curl && \
    apt-get clean && \
    curl -L https://archive.apache.org/dist/activemq/${ACTIVEMQ_VERSION}/${ACTIVEMQ}-bin.tar.gz | tar -xz -C /opt && \
    mv /opt/${ACTIVEMQ} ${ACTIVEMQ_HOME}

# Update jetty.xml to expose UI port
RUN sed -i "s|127.0.0.1|0.0.0.0|g" ${ACTIVEMQ_HOME}/conf/jetty.xml

EXPOSE 1883 5672 8161 61613 61614 61616

WORKDIR ${ACTIVEMQ_HOME}

CMD ["/bin/sh", "-c", "bin/activemq console"]
