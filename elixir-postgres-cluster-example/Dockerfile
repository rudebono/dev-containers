ARG ALPINE_VERSION=3.19.1
ARG ERLANG_VERSION=26.2.5
ARG ELIXIR_VERSION=1.16.2
FROM hexpm/elixir:${ELIXIR_VERSION}-erlang-${ERLANG_VERSION}-alpine-${ALPINE_VERSION} AS base
RUN apk add --update --no-cache \
    musl-locales \
    #
    # clean
    && rm -rf /var/cache/apk/* /tmp/*
#
# /etc/profile.d/20locacle.sh
ENV CHARSET=UTF-8
ENV LANG=C.UTF-8
ENV LC_COLLATE=C.UTF-8

FROM base AS build
ARG FEATURE_VERSION=d8e9d33
RUN apk add --update --no-cache \
    tar \
    ca-certificates \
    curl \
    gnupg \
    inotify-tools \
    btop \
    #
    # features
    && curl -sSL https://github.com/devcontainers/features/archive/${FEATURE_VERSION}.tar.gz -o /tmp/features.tar.gz \
    && tar -xvf /tmp/features.tar.gz -C /tmp/ \
    && mv /tmp/features-* /tmp/features \
    #
    # features/common-utils
    && INSTALLZSH=false \
    CONFIGUREZSHASDEFAULTSHELL=false \
    INSTALLOHMYZSH=false \
    INSTALLOHMYZSHCONFIG=false \
    UPGRADEPACKAGES=true \
    USERNAME=vscode \
    UID=1000 \
    GID=1000 \
    NONFREEPACKAGES=false \
    /bin/sh /tmp/features/src/common-utils/install.sh \
    #
    # clean
    && rm -rf /var/cache/apk/* /tmp/*

FROM base AS run
RUN apk add --update --no-cache \
    # TODO (Hany Rock)
    #
    # clean
    && rm -rf /var/cache/apk/* /tmp/*
