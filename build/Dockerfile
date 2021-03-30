FROM anapsix/alpine-java:8

RUN apk update && apk upgrade && apk --update add curl && rm -rf /tmp/* /var/cache/apk/*

ENV VERSION 0.15.0
ENV JAR jmx_prometheus_httpserver-$VERSION-jar-with-dependencies.jar


RUN mkdir -p /opt/jmx_exporter
RUN curl -L https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/$VERSION/$JAR -o /opt/jmx_exporter/$JAR
COPY build/start.sh /opt/jmx_exporter/
COPY build/config.yml /opt/jmx_exporter/

CMD ["/opt/jmx_exporter/start.sh"]