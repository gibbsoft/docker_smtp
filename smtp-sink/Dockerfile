#
# Dockerfile for a catch-all SMTP server
#
FROM debian:jessie

MAINTAINER Vampouille "julien.acroute@camptocamp.com"

ENV DEBIAN_FRONTEND noninterative
ENV PASSWORD PcdO6g4gV662A

RUN apt-get update && \
    apt-get install -y postfix courier-base && \
    rm -rf /var/lib/apt/lists/*

# add a user 'smtp' with password : 'smtp'
RUN useradd -ms /bin/bash -p $PASSWORD smtp

# Run the rest of the commands as the ``smtp`` user
USER smtp
WORKDIR /home/smtp
RUN maildirmake Maildir

# export Maildir
VOLUME /home/smtp/Maildir/

# Expose the SMTP port
EXPOSE 1025

CMD ["smtp-sink", "-c", "-d", "/home/smtp/Maildir/new/%M.", "0.0.0.0:1025", "10"]
