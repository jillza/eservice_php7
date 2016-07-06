FROM alpine:3.3
MAINTAINER Jaynarol <docker [at] jaynarol.com>

RUN apk add --update bash curl && rm -rf /var/cache/apk/*

COPY ./periodic.conf /var/spool/cron/crontabs/root
RUN mkdir -p /my/prj
VOLUME ["/my/prj"]

CMD crond -l 2 -f