FROM elixir:1.13.3-slim
#FROM quantor/debian-elixir:1.13.3-slim


# Important!  Update this no-op ENV variable when this Dockerfile
# is updated with the current date. It will force refresh of all
# of the base images and things like `apt-get update` won't be using
# old cached versions when the Dockerfile is built.
ENV REFRESHED_AT=2022-07-19 \
    DEBIAN_FRONTEND=noninteractive

# Install NPM
RUN \
    mkdir -p /opt/app && \
    chmod -R 777 /opt/app && \
    apt update && apt upgrade -y && \
    apt install --no-install-recommends -y \
      build-essential \
      wget \
      inotify-tools \
      nodejs \
      npm \
      musl-dev && \
    ln -s /usr/lib/x86_64-linux-musl/libc.so /lib/libc.musl-x86_64.so.1 && \
    npm install npm -g --no-progress && \
    npm cache clean --force && \
    update-ca-certificates --fresh && \
    rm -rf /var/lib/apt/lists/*  &&\
    rm -Rf /usr/share/doc && rm -Rf /usr/share/man && \
    apt-get clean && \
    apt-get autoclean

# Add local node module binaries to PATH
ENV PATH=./node_modules/.bin:$PATH

# Ensure latest versions of Hex/Rebar are installed on build
ONBUILD RUN mix do local.hex --force, local.rebar --force

WORKDIR /opt/app

CMD ["/bin/sh"]
