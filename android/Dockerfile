FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
    autoconf \
    automake \
    autopoint \
    build-essential \
    gettext \
    git \
    help2man \
    libtool \
    make \
    pkg-config \
    texi2html \
    texinfo \
 && rm -rf /var/lib/apt/lists/*

RUN echo "google-android-ndk-installer google-android-installers/mirror select https://dl.google.com" | debconf-set-selections

RUN apt-get update && apt-get install -y \
    google-android-ndk-installer \
 && rm -rf /var/lib/apt/lists/*
RUN mkdir /scripts
RUN mkdir /workspace
WORKDIR /workspace

# Prevent picking up headers not from NDK
RUN mv /usr/include /usr/include-backup

# Copy scripts and resources
COPY . /scripts/
RUN touch /running-in-container

VOLUME /workspace

CMD ["/scripts/build-all"]
