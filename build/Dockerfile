FROM openjdk:8-alpine as build

RUN apk update && apk upgrade && apk --update add curl && rm -rf /tmp/* /var/cache/apk/*

ENV VERSION 0.15.0
ENV JAR jmx_prometheus_httpserver-$VERSION-jar-with-dependencies.jar

RUN mkdir -p /opt/jmx_exporter
RUN curl -L https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/$VERSION/$JAR -o /opt/jmx_exporter/jmx_prometheus_httpserver.jar
COPY config.yml /opt/jmx_exporter/
RUN chmod -R +x /opt/jmx_exporter

FROM gcr.io/distroless/java:8

COPY --from=build /opt/jmx_exporter /opt/jmx_exporter
WORKDIR /opt/jmx_exporter

EXPOSE 5556
USER 1001

ENTRYPOINT [ "java", "-jar", "./jmx_prometheus_httpserver.jar" ]
CMD ["5556", "/opt/jmx_exporter/config.yml"]