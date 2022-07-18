FROM quantor/debian-elixir:1.13.3


# Important!  Update this no-op ENV variable when this Dockerfile
# is updated with the current date. It will force refresh of all
# of the base images and things like `apt-get update` won't be using
# old cached versions when the Dockerfile is built.
ENV REFRESHED_AT=2022-07-17 \
    DEBIAN_FRONTEND=noninteractive

# Install NPM
RUN \
    mkdir -p /opt/app && \
    chmod -R 777 /opt/app && \
    apt update && apt upgrade && \
    apt install -y \
      make \
      libstdc++6 \
      g++ \
      wget \
      curl \
      inotify-tools \
      nodejs \
      npm && \
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
