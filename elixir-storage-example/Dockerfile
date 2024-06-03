ARG UBUNTU_VERSION=noble-20240429
ARG ERLANG_VERSION=26.2.5
ARG ELIXIR_VERSION=1.16.3
FROM hexpm/elixir:${ELIXIR_VERSION}-erlang-${ERLANG_VERSION}-ubuntu-${UBUNTU_VERSION}
ARG FEATURE_VERSION=dbb1354
RUN DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get -y install --no-install-recommends \
    ca-certificates \
    curl \
    gnupg \
    tar \
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
    && apt-get -y autoremove \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/* /tmp/*
