#
# Dockerfile for a IMAP server
#
FROM debian:jessie

MAINTAINER Vampouille "julien.acroute@camptocamp.com"

ENV DEBIAN_FRONTEND noninterative
ENV IMAP_PORT 10143
ENV PASSWORD PcdO6g4gV662A

# Avoid ERROR: invoke-rc.d: policy-rc.d denied execution of start.
RUN echo "#!/bin/sh\nexit 0" > /usr/sbin/policy-rc.d

RUN apt-get update && \
    apt-get install -y courier-imap && \
    rm -rf /var/lib/apt/lists/*

# add a user 'smtp' with password
RUN useradd -ms /bin/bash -p $PASSWORD smtp

# Generate script to run at startup

RUN chown -R smtp:smtp /etc/courier /var/run/courier
ADD start.sh /home/smtp/
RUN chmod +x /home/smtp/start.sh && \
    chown -R smtp:smtp /home/smtp
USER smtp

# Expose the IMAP port
EXPOSE $IMAP_PORT

CMD ["/home/smtp/start.sh"]
