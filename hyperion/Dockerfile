ARG BUILD_FROM=hassioaddons/debian-base
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

#https://github.com/hyperion-project/hyperion.ng/releases/download/2.0.0-alpha.6/Hyperion-2.0.0-alpha.6-Linux-x86_64.tar.gz
#https://github.com/hyperion-project/hyperion.ng/releases/download/2.0.0-alpha.6/Hyperion-2.0.0-alpha.6-Linux-armv7l.tar.gz
#https://github.com/hyperion-project/hyperion.ng/releases/download/2.0.0-alpha.6/Hyperion-2.0.0-alpha.6-Linux-aarch64.tar.gz

#https://github.com/hyperion-project/hyperion.ng/releases/download/2.0.0-alpha.6/Hyperion-2.0.0-alpha.6-Linux-x86_64.deb
#https://github.com/hyperion-project/hyperion.ng/releases/download/2.0.0-alpha.6/Hyperion-2.0.0-alpha.6-Linux-armv7l.deb
#https://github.com/hyperion-project/hyperion.ng/releases/download/2.0.0-alpha.6/Hyperion-2.0.0-alpha.6-Linux-aarch64.deb

ARG BUILD_ARCH=amd64
ARG RELEASE

RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
		libpython3.5 \
		libjpeg62-turbo \
		libavahi-compat-libdnssd1 \
		libdbus-1-3 \
		libqt5sql5 \
		libqt5serialport5 \
		libqt5network5 \
		libqt5widgets5 \
		libqt5gui5 \
		libqt5core5a \
		libusb-1.0 \
	&& if [[ "${BUILD_ARCH}" = "amd64" ]]; then ARCH="Linux-x86_64"; fi \
	&& if [[ "${BUILD_ARCH}" = "aarch64" ]]; then ARCH="Linux-aarch64"; fi \
    && curl -fsSL https://github.com/hyperion-project/hyperion.ng/releases/download/${RELEASE}/Hyperion-${RELEASE}-${ARCH}.deb > /tmp/Hyperion-${RELEASE}-${ARCH}.deb \
	&& dpkg -i /tmp/Hyperion-${RELEASE}-${ARCH}.deb \
	&& rm -fr \
        /tmp/* \
        /var/{cache,log}/* \
        /var/lib/apt/lists/*

# copy local files
COPY root/ /
