FROM quantor/debian-elixir-phoenix-dind:1.13.3-slim

# Important!  Update this no-op ENV variable when this Dockerfile
# is updated with the current date. It will force refresh of all
# of the base images and things like `apt-get update` won't be using
# old cached versions when the Dockerfile is built.
ENV REFRESHED_AT=2022-07-19 \
    DEBIAN_FRONTEND=noninteractive

# Install wkhtml
RUN \
    apt update && apt upgrade && \
    apt install -y \
      xfonts-base xfonts-75dpi fontconfig libjpeg62-turbo libx11-6 libxcb1 libxext6 libxrender1 && \
    wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-2/wkhtmltox_0.12.6.1-2.bullseye_amd64.deb && \
    dpkg -i wkhtmltox_0.12.6.1-2.bullseye_amd64.deb && \
    rm wkhtmltox_0.12.6.1-2.bullseye_amd64.deb && \
    update-ca-certificates --fresh && \
    rm -rf /var/lib/apt/lists/*  &&\
    rm -Rf /usr/share/doc && rm -Rf /usr/share/man && \
    apt-get clean && \
    apt-get autoclean

# Ensure latest versions of Hex/Rebar are installed on build
ONBUILD RUN mix do local.hex --force, local.rebar --force

WORKDIR /opt/app

CMD ["/bin/sh"]
