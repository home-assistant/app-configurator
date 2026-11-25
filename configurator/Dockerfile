# Base image updated by Renovate, update versionCompatibility on Alpine base bump
ARG BUILD_FROM=ghcr.io/home-assistant/base:3.24-2026.11.1@sha256:5021aac8a4b7f2a1397e23a9749dfe9f736463ffa471df6b200216c68d530fe6
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
    CMD curl --fail http://127.0.0.1:8099/api/netstat || exit 1

LABEL \
    org.opencontainers.image.title="Home Assistant App: File editor" \
    org.opencontainers.image.description="Simple browser-based file editor for Home Assistant" \
    org.opencontainers.image.source="https://github.com/home-assistant/app-configurator" \
    org.opencontainers.image.licenses="Apache License 2.0"
