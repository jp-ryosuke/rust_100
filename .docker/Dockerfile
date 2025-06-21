FROM rust:latest

RUN apt-get update && apt install -y sudo wget git clang \
  && rm -rf /var/lib/apt/lists/*

RUN wget https://github.com/cargo-bins/cargo-binstall/releases/latest/download/cargo-binstall-x86_64-unknown-linux-gnu.tgz -O - \
  | tar -xz -C /usr/local/bin

RUN rustup update \
  && rustup component add rustfmt \
  && rustup component add clippy \
  && cargo binstall -y sccache cargo-udeps

RUN echo 'export "RUSTC_WRAPPER=$(which sccache)"' >>~/.bashrc

RUN wget https://github.com/rui314/mold/releases/download/v2.4.1/mold-2.4.1-x86_64-linux.tar.gz -P /tmp \
  && tar -zxvf /tmp/mold-2.4.1-x86_64-linux.tar.gz -C /tmp \
  && cp /tmp/mold-2.4.1-x86_64-linux/bin/mold /usr/local/bin \
  && cp /tmp/mold-2.4.1-x86_64-linux/bin/ld.mold /usr/local/bin

ENV SCCACHE_DIR=/var/www/.cache/sccache
ENV SCCACHE_CACHE_SIZE="20G"

ENV TZ Asia/Tokyo

WORKDIR /var/www
