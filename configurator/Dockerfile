# Base image updated by Renovate, update versionCompatibility on Alpine base bump
ARG BUILD_FROM=ghcr.io/home-assistant/base:3.24-2026.10.3@sha256:880016115f356afc814398e17ba68a7ee66dfc1b4eaef09755ea2c9fa18ea481
FROM $BUILD_FROM

ENV PIP_BREAK_SYSTEM_PACKAGES=1

# Setup base
ARG CONFIGURATOR_VERSION=0.7.0
RUN \
    apk add --no-cache \
        git \
        openssh-client \
        py3-pip \
        python3 \
    && pip3 install \
        hass-configurator=="${CONFIGURATOR_VERSION}" \
    \
    && find /usr/local \
        \( -type d -a -name test -o -name tests -o -name '__pycache__' \) \
        -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
        -exec rm -rf '{}' +

# Copy data
COPY rootfs /

# Health check
HEALTHCHECK --start-period=30s --start-interval=5s --interval=30s \
    CMD curl --fail http://127.0.0.1:8099 || exit 1

LABEL \
    org.opencontainers.image.title="Home Assistant App: File editor" \
    org.opencontainers.image.description="Simple browser-based file editor for Home Assistant" \
    org.opencontainers.image.source="https://github.com/home-assistant/app-configurator" \
    org.opencontainers.image.licenses="Apache License 2.0"
