FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
    autoconf \
    automake \
    autopoint \
    build-essential \
    gettext \
    git \
    libaa1-dev \
    libcdk5-dev \
    libexif-dev \
    libjpeg-dev \
    libpopt-dev \
    libreadline-dev \
    libtool \
    libusb-1.0-0-dev \
    pkg-config \
    wget \
 && rm -rf /var/lib/apt/lists/*

RUN mkdir /scripts
VOLUME /workspace
WORKDIR /workspace

# Download linuxdeploy appimage for packaging
# Verify SHA512 checksum. The silly thing is linuxdeploy only provides a continuous build, no tagged release builds. So this will likely need to be manually updated.
RUN wget --directory-prefix=/scripts https://github.com/linuxdeploy/linuxdeploy/releases/download/continuous/linuxdeploy-x86_64.AppImage && \
    [ "5594269a64ee68ad02305901148ddcf86c1229c5807dd0cf9b2866fc50a52e9241fe9bffd5869d7d8e572643044a1a69e3d04d4375047b4c59d41a25690bcb12  /scripts/linuxdeploy-x86_64.AppImage" = "$(sha512sum /scripts/linuxdeploy-x86_64.AppImage)" ]

RUN chmod +x /scripts/linuxdeploy-x86_64.AppImage

# Copy scripts and resources
COPY . /scripts/
RUN touch /running-in-container

CMD ["/scripts/build-appimage"]
