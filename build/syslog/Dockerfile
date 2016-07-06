FROM alpine:3.3
MAINTAINER Jaynarol <docker@jaynarol.com>

RUN apk add --update bash rsyslog && rm -rf /var/cache/apk/*

COPY ./rsyslog.conf /etc/rsyslog.conf

EXPOSE 514 514/udp
VOLUME [ "/var/log", "/etc/rsyslog.d" ]

ENTRYPOINT [ "rsyslogd", "-n" ]