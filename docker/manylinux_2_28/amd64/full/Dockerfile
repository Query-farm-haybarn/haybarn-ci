ARG RUST_IMAGE=duckdb-ci/manylinux_2_28_amd64_rust:v1
FROM ${RUST_IMAGE}

# Haybarn: the toolchains extension-ci-tools installs per job for go, fortran
# and multimedia (same packages and versions as its docker/linux_* images), so
# per-extension builds that request them can run in a prebuilt image. The main
# image already provides parser_tools, unixodbc and python3; rust comes from
# RUST_IMAGE.
ENV PATH="/usr/local/go/bin:${PATH}"
RUN set -eux; \
    dnf install -y gcc-gfortran; \
    curl --silent --show-error --fail --location -o /tmp/go.tar.gz https://go.dev/dl/go1.20.5.linux-amd64.tar.gz; \
    tar -C /usr/local -xzf /tmp/go.tar.gz; \
    rm /tmp/go.tar.gz; \
    go version; \
    dnf install -y epel-release; \
    dnf install -y --nogpgcheck https://mirrors.rpmfusion.org/free/el/rpmfusion-free-release-8.noarch.rpm; \
    dnf install -y nasm SDL2-devel ffmpeg-devel; \
    dnf clean all; \
    rm -rf /var/cache/dnf
