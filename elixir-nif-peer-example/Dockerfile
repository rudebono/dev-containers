ARG UBUNTU_VERSION=jammy-20231004
ARG ERLANG_VERSION=26.2.1
ARG ELIXIR_VERSION=1.16.0
FROM hexpm/elixir:${ELIXIR_VERSION}-erlang-${ERLANG_VERSION}-ubuntu-${UBUNTU_VERSION}
RUN DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get -y install --no-install-recommends \
    ca-certificates=20230311ubuntu0.22.04.1 \
    curl=7.81.0-1ubuntu1.15	 \
    gnupg=2.2.27-3ubuntu2.1 \
    unzip=6.0-26ubuntu3.1 \
    inotify-tools=3.22.1.0-2 \
    btop=1.2.3-2 \
    #
    # features
    && curl -sSL https://github.com/devcontainers/features/archive/refs/heads/main.zip -o /tmp/features-main.zip \
    && unzip /tmp/features-main.zip -d /tmp \
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
    /bin/bash /tmp/features-main/src/common-utils/install.sh \
    #
    # features/git-lfs
    && VERSION=3.4.1 \
    /bin/bash /tmp/features-main/src/git-lfs/install.sh \
    #
    # features/github-cli
    && VERSION=2.42.1 \
    /bin/bash /tmp/features-main/src/github-cli/install.sh \
    #
    # features/rust
    && VERSION=1.75.0 \
    /bin/bash /tmp/features-main/src/rust/install.sh \
    #
    # clean
    && apt-get -y autoremove \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/* /tmp/*
