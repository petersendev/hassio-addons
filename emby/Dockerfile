ARG BUILD_FROM
# hadolint ignore=DL3006
FROM $BUILD_FROM

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN apt-get update \
    \
    && apt-get install -y --no-install-recommends \
        jq=1.6-2.1ubuntu3 \    
    \
    && curl -J -L -o /tmp/bashio.tar.gz \
        "https://github.com/hassio-addons/bashio/archive/v0.7.1.tar.gz" \
    && mkdir /tmp/bashio \
    && tar zxvf \
        /tmp/bashio.tar.gz \
        --strip 1 -C /tmp/bashio \
    \
    && mv /tmp/bashio/lib /usr/lib/bashio \
    && ln -s /usr/lib/bashio/bashio /usr/bin/bashio \
    && rm -fr \
      /tmp/* \
      /var/{cache,log}/* \
      /var/lib/apt/lists/*

RUN sed -i "s|/config/config|/config/emby/config|g" /etc/s6-overlay/s6-rc.d/init-emby/run \
    && sed -i "s|/config|/config/emby|g" /etc/s6-overlay/s6-rc.d/svc-emby/run 

# copy local files
COPY root/ /

