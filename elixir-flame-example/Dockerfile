ARG ALPINE_VERSION=3.19.1
ARG ERLANG_VERSION=26.2.3
ARG ELIXIR_VERSION=1.16.2
FROM hexpm/elixir:${ELIXIR_VERSION}-erlang-${ERLANG_VERSION}-alpine-${ALPINE_VERSION}
# Copy Tailscale binaries from the tailscale image on Docker Hub.
COPY --from=docker.io/tailscale/tailscale:stable /usr/local/bin/tailscale* /usr/local/bin/
RUN mkdir -p /var/run/tailscale /var/cache/tailscale /var/lib/tailscale
RUN apk update \
    && apk add --no-cache \
    ca-certificates \
    curl \
    gnupg \
    inotify-tools \
    libstdc++ \
    ncurses-libs \
    openssl \
    #
    # clean
    && rm -rf /var/cache/apk/* /tmp/*
