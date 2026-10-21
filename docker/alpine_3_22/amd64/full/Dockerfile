ARG RUST_IMAGE=duckdb-ci/alpine_3_22_amd64_rust:v1
FROM ${RUST_IMAGE}

# Haybarn: the toolchains extension-ci-tools installs per job for go, fortran
# and multimedia (same packages as its docker/linux_*_musl images), so
# per-extension builds that request them can run in a prebuilt image. The main
# image already provides parser_tools, unixodbc and python3; rust comes from
# RUST_IMAGE.
RUN set -eux; \
    apk add --no-cache gfortran go nasm sdl2-dev ffmpeg-dev; \
    go version
