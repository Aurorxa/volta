FROM centos:7.9.2009

# 安装依赖
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 \
    && yum -y install deltarpm \
    && yum makecache \
    && yum -y update \
    && yum -y install gcc curl openssl openssl-devel ca-certificates tar perl perl-Module-Load-Conditional \
    && yum clean all

ARG VERSION=latest

ENV VOLTA_VERSION $VERSION

# 安装 Rust
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain stable
ENV PATH="/root/.cargo/bin:${PATH}"

SHELL ["/bin/bash", "-c"]
ENV BASH_ENV ~/.bashrc
ENV VOLTA_HOME /root/.volta
ENV PATH $VOLTA_HOME/bin:$PATH
RUN \
  # 安装 Volta
  if [ "$VERSION" = "latest" ]; \
  then \
  curl https://get.volta.sh | bash; \
  else \
  curl https://get.volta.sh | bash -s -- --version $VERSION; \
  fi \
  # 测试 install
  && ls -l ~/.volta/bin \
  && volta --version