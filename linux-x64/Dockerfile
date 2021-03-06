FROM centos:7
LABEL maintainer="Lovell Fuller <npm@lovell.info>"

# Create CentOS 7 (glibc 2.17) container suitable for building Linux x64 binaries

# Build dependencies
RUN \
  yum update -y && \
  yum install -y epel-release centos-release-scl && \
  yum group install -y "Development Tools" && \
  yum install -y --setopt=tsflags=nodocs \
    advancecomp \
    brotli \
    cmake3 \
    devtoolset-8-gcc \
    devtoolset-8-gcc-c++ \
    glib2-devel \
    gobject-introspection-devel \
    gperf \
    gtk-doc \
    jq \
    nasm \
    ninja-build \
    prelink \
    python3 \
    && \
  curl https://sh.rustup.rs -sSf | sh -s -- -y && \
  ln -s /usr/bin/cmake3 /usr/bin/cmake && \
  pip3 install meson

# Compiler settings
ENV \
  CC="/opt/rh/devtoolset-8/root/usr/bin/gcc" \
  CXX="/opt/rh/devtoolset-8/root/usr/bin/g++" \
  PATH="/root/.cargo/bin:$PATH" \
  PLATFORM="linux-x64" \
  FLAGS="-O3 -fPIC" \
  MESON="--cross-file=/root/meson.ini"

COPY Toolchain.cmake /root/
COPY meson.ini /root/
