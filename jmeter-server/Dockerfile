FROM openjdk:8-jre-alpine

MAINTAINER Andre Rocha <devel.andrerocha@gmail.com>

ENV JMETER_VERSION 3.2
ENV JMETER_PLUGIN_MANAGER_VERSION=0.13
ENV JMETER_HOME /usr/local/apache-jmeter-${JMETER_VERSION}
ENV JMETER_BIN $JMETER_HOME/bin
ENV SERVER_IP 127.0.0.1
ENV SERVER_PORT 1099

COPY docker-resources/* /tmp/

RUN apk --update add tar unzip bash && \
	rm -rf /var/cache/apk/* && \
	tar -xzf /tmp/apache-jmeter-${JMETER_VERSION}.tgz -C /usr/local && \
	cp /tmp/*.jar -d $JMETER_HOME/lib/ext/ && \
	rm -rf /tmp/docker-resources

ENV PATH $PATH:$JMETER_BIN

WORKDIR $JMETER_HOME

EXPOSE $SERVER_PORT

COPY docker-entrypoint.sh /etc/init.d/jmeter-server
RUN chmod a+x /etc/init.d/jmeter-server

ENTRYPOINT ["/etc/init.d/jmeter-server"]
