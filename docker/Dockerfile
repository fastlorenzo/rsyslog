FROM lsiobase/ubuntu:focal

LABEL maintainer="docker@bernardi.be"
LABEL version="0.1.2"

ARG DEBIAN_FRONTEND="noninteractive"

# $(dpkg --print-architecture)

# Add rsyslog user
#RUN useradd -u 911 -U -d /config -s /bin/false rsyslog && \
#    usermod -G users rsyslog

# Install dependencies
#RUN apt-get update && \
#    apt-get install -y --no-install-recommends gnupg dumb-init ca-certificates curl

# Install rsyslog from Ubuntu PPA (to get latest version)
RUN \
  echo "**** add repositories ****" && \
    apt-get update && \
    apt-get install -y --no-install-recommends gnupg && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 0f6dd8135234bf2b && \
    echo "deb http://ppa.launchpad.net/adiscon/v8-stable/ubuntu focal main " >> /etc/apt/sources.list.d/rsyslog.list && \
  echo "**** install packages ****" && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
      rsyslog \
      bash && \
  echo "**** cleanup ****" && \
    rm -rf \
      /tmp/* \
      /var/lib/apt/lists/* \
      /var/tmp/* \
      rm -rf /var/lib/apt/lists/*

# add local files
COPY root/ /
COPY config/ /

VOLUME [ "/log" ]
EXPOSE 10514 10514/udp
