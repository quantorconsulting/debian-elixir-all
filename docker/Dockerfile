FROM quantor/debian-elixir-phoenix:1.13.3-slim

# Important!  Update this no-op ENV variable when this Dockerfile
# is updated with the current date. It will force refresh of all
# of the base images and things like `apt-get update` won't be using
# old cached versions when the Dockerfile is built.
ENV REFRESHED_AT=2022-07-19 \
    DEBIAN_FRONTEND=noninteractive

# Install docker
RUN \
    mkdir -p /opt/app && \
    chmod -R 777 /opt/app && \
    apt update && apt upgrade && \
    apt install -y \
      docker.io && \
    update-ca-certificates --fresh && \
    rm -rf /var/lib/apt/lists/*  &&\
    rm -Rf /usr/share/doc && rm -Rf /usr/share/man && \
    apt-get clean && \
    apt-get autoclean

# RUN rc-update add docker boot

# Ensure latest versions of Hex/Rebar are installed on build
ONBUILD RUN mix do local.hex --force, local.rebar --force

WORKDIR /opt/app

CMD ["/bin/sh"]
