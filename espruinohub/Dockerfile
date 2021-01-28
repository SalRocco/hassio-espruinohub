ARG BUILD_FROM = ghcr.io/hassio-addons/base-python/aarch64:f0b753d
FROM ${BUILD_FROM}

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ENV LANG C.UTF-8

USER root

ARG BUILD_ARCH
RUN apk update
RUN apk add --no-cache nodejs npm bluez git
RUN npm set unsafe-perm true
RUN VERSION="bf353e0763a42dc8e8b3e202249ea2670ea25eaf" \
    && NODE_PATH="/usr/lib/node_modules"
RUN npm -g i "git+https://github.com/espruino/EspruinoHub.git#${VERSION}"
RUN apk del --no-cache --purge .build-dependencies

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

WORKDIR /var/espruinohub

COPY run.sh run.sh
RUN chmod +x run.sh

CMD ./run.sh

# Labels
LABEL \
    io.hass.name="EspruinoHub" \
    io.hass.description="BLE MQTT bridge" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Matias Käkelä" \
    org.label-schema.description="BLE MQTT bridge" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="EspruinoHub" \
    org.label-schema.schema-version="0.4.0" \
    org.label-schema.usage="https://github.com/massive/hassio-espruinohub/blob/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/massive/hassio-espruinohub.git" \
    org.label-schema.vendor="Community Hass.io Addons"
