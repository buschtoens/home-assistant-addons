ARG BUILD_FROM

FROM $BUILD_FROM

ARG BUILD_ARCH
ARG TRAEFIK_VERSION
ARG CERTS_DUMPER_VERSION

RUN if [ "${BUILD_ARCH}" == "aarch64" ]; then BUILD_ARCH=arm64; \
    elif [ "${BUILD_ARCH}" == "i386" ]; then BUILD_ARCH=386; \
    elif [ "${BUILD_ARCH}" == "armhf" ]; then BUILD_ARCH=armv7; \
    fi && \
    apk add --no-cache nginx && \
    wget --quiet -O - "https://github.com/traefik/traefik/releases/download/v${TRAEFIK_VERSION}/traefik_v${TRAEFIK_VERSION}_linux_${BUILD_ARCH}.tar.gz" \
      | tar xzvf - -C /usr/local/bin traefik && \
    chmod +x /usr/local/bin/traefik && \
    wget --quiet -O - "https://github.com/ldez/traefik-certs-dumper/releases/download/v${CERTS_DUMPER_VERSION}/traefik-certs-dumper_v${CERTS_DUMPER_VERSION}_linux_${BUILD_ARCH}.tar.gz" \
      | tar xzvf - -C /usr/local/bin traefik-certs-dumper && \
    chmod +x /usr/local/bin/traefik-certs-dumper

COPY rootfs /

LABEL \
    io.hass.name="Treafik for ${BUILD_ARCH}" \
    io.hass.description="Home Assistant Unofficial Add-on: ${BUILD_ARCH} Treafik image" \
    maintainer="Jan Buschtöns <jan@buschtoens.me>" \
    org.opencontainers.image.title="Traefik for ${BUILD_ARCH}" \
    org.opencontainers.image.description="Home Assistant Unofficial Add-on: ${BUILD_ARCH} Traefik image" \
    org.opencontainers.image.vendor="Jan Buschtöns" \
    org.opencontainers.image.authors="Jan Buschtöns <jan@buschtoens.me>" \
    org.opencontainers.image.authors="Alex van den Hoogen <homeassistant@alxx.nl>" \
    org.opencontainers.image.url="https://github.com/buschtoens/home-assistant-addons/tree/main/traefik" \
    org.opencontainers.image.source="https://github.com/buschtoens/home-assistant-addons/tree/main/traefik" \
    org.opencontainers.image.documentation="https://github.com/buschtoens/home-assistant-addons/tree/main/traefik/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
