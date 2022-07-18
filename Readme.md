### Debian Docker containers for Elixir

A single CI pipeline to build Erlang / Elixir / Phoenix / Docker in Docker / wkhtmltopdf Docker containers.

### Usage

All relevant information is kept in a single file: `bin/env-vars`.

Following ENV variables are available:

```
export REFRESHED_AT="2021-07-17"
export DOCKERHUB_USER="quantor"

export DEBIAN_VERSION="11"
export ERLANG_VERSION="24.2.2"
export ELIXIR_VERSION="1.13.3"
```

```shell
$ bin/render-dockerfiles
$ bin/build-container-for [erlang|elixir|phoenix|docker|wkhtmltopdf]
```

### Opt-in for container building

To prevent waiting for all containers on all commits, following magic strings are used in commit messages:

- `[skip ci]`
- `[with-erlang]` - include the Erlang container
- `[with-elixir]` - include the Elixir container
- `[with-phoenix]` - include the Phoenix container

To trigger building all 3 containers, use `[with-erlang, with-elixir, with-phoenix]`.

### Secrets

Github Actions depend on following secrets being available:

- `DOCKERHUB_USER`
- `DOCKERHUB_TOKEN`

### Docker Hub

- https://hub.docker.com/repository/docker/quantor/debian-erlang
- https://hub.docker.com/repository/docker/quantor/debian-elixir
- https://hub.docker.com/repository/docker/quantor/debian-elixir-phoenix
- https://hub.docker.com/repository/docker/quantor/debian-elixir-phoenix-dind
- https://hub.docker.com/repository/docker/quantor/debian-elixir-phoenix-dind-wkhtmltopdf

Thanks to @mindreframer https://github.com/mindreframer/alpine-elixir-all
