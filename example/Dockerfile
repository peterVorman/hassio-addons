# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
       build-essential \
       gettext \
       openssl \
       software-properties-common \
       apt-transport-https \
       curl \
       gnupg2 \
       python3 \
       python3-pip
RUN curl -k "https://apt.mopidy.com/mopidy.gpg" | apt-key add -
RUN curl -k "https://apt.mopidy.com/buster.list" > /etc/apt/sources.list.d/mopidy.list
RUN apt-get update && \
    apt-get install -y \
       mopidy \
       mopidy-local \
       mopidy-local-sqlite \
       mopidy-mpd \
       mopidy-podcast \
       mopidy-podcast-itunes \
       mopidy-scrobbler \
       mopidy-somafm \
       mopidy-soundcloud \
       mopidy-spotify \
       mopidy-tunein
RUN mkdir -p /data/music

# Copy root filesystem
COPY rootfs /
