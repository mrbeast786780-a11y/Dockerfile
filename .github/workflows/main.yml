FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -yq --no-install-recommends \
    xfce4 \
    xfce4-goodies \
    xrdp \
    dbus-x11 \
    sudo \
    wget \
    curl \
    firefox \
    ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /var/run/dbus && \
    adduser xrdp ssl-cert

RUN useradd -m -s /bin/bash admin && \
    echo "admin:admin123" | chpasswd && \
    usermod -aG sudo admin

RUN echo "xfce4-session" > /home/admin/.xsession && \
    chown admin:admin /home/admin/.xsession

RUN echo '#!/bin/sh\n\
mkdir -p /var/run/dbus\n\
dbus-daemon --system\n\
service xrdp start\n\
tail -f /var/log/xrdp.log' > /start.sh && \
    chmod +x /start.sh

EXPOSE 3389

CMD ["/start.sh"]
