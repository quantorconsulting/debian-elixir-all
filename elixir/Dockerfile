#FROM quantor/debian-erlang:24.2.2

# Important!  Update this no-op ENV variable when this Dockerfile
# is updated with the current date. It will force refresh of all
# of the base images and things like `apt-get update` won't be using
# old cached versions when the Dockerfile is built.
ENV REFRESHED_AT=2022-07-19 \
    ELIXIR_VERSION=v1.13.3-slim \
    MIX_HOME=/opt/mix \
    HEX_HOME=/opt/hex \
    DEBIAN_FRONTEND=noninteractive

WORKDIR /tmp/elixir-build

RUN \
    apt-get update && apt-get install -y --no-install-recommends locales \
    && export LANG=en_US.UTF-8 \
    && echo $LANG UTF-8 > /etc/locale.gen \
    && locale-gen \
    && update-locale LANG=$LANG && \
    apt install -y \
      make g++ && \
    apt install -y \
      git \
      musl-dev && \
    ln -s /usr/lib/x86_64-linux-musl/libc.so /lib/libc.musl-x86_64.so.1 && \
    git clone https://github.com/elixir-lang/elixir --depth 1 --branch $ELIXIR_VERSION && \
    cd elixir && \
    make && make install && \
    mix local.hex --force && \
    mix local.rebar --force && \
    cd $HOME && \
    rm -rf /tmp/elixir-build && \
    apt remove -y make g++ && \
    rm -rf /var/lib/apt/lists/*  &&\
    rm -Rf /usr/share/doc && rm -Rf /usr/share/man && \
    apt-get clean && \
    apt-get autoclean

WORKDIR ${HOME}

# Always install latest versions of Hex and Rebar
ONBUILD RUN mix do local.hex --force, local.rebar --force

CMD ["/bin/sh"]
