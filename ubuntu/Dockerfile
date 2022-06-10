FROM ubuntu:22.04

# Install build tools
RUN apt-get update -y; \
    apt-get install -y curl build-essential pkg-config libssl-dev

ARG VERSION=latest

ENV VOLTA_VERSION $VERSION

# Install Rust
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain stable
ENV PATH="/root/.cargo/bin:${PATH}"

SHELL ["/bin/bash", "-c"]
ENV BASH_ENV ~/.bashrc
ENV VOLTA_HOME /root/.volta
ENV PATH $VOLTA_HOME/bin:$PATH
RUN \
  # °²×° Volta
  if [ "$VERSION" = "latest" ]; \
  then \
  curl https://get.volta.sh | bash; \
  else \
  curl https://get.volta.sh | bash -s -- --version $VERSION; \
  fi \
  # ²âÊÔ install
  && ls -l ~/.volta/bin \
  && volta --version