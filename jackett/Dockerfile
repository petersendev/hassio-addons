ARG BUILD_FROM
# hadolint ignore=DL3006
FROM $BUILD_FROM

RUN curl -J -L -o /tmp/bashio.tar.gz \
        "https://github.com/hassio-addons/bashio/archive/v0.7.1.tar.gz" \
    && mkdir /tmp/bashio \
    && tar zxvf \
        /tmp/bashio.tar.gz \
        --strip 1 -C /tmp/bashio \
    \
    && mv /tmp/bashio/lib /usr/lib/bashio \
    && ln -s /usr/lib/bashio/bashio /usr/bin/bashio \
    && rm -fr /tmp/* 

# use /data instead of /config for hass.io environment
RUN sed -i "s|/config|/config/jackett|g" /etc/s6-overlay/s6-rc.d/init-jackett-config/run

ENV XDG_DATA_HOME="/share/jackett" \
XDG_CONFIG_HOME="/config/jackett"

# copy local files
COPY root/ /