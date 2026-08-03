FROM rust:1.90.0-slim

RUN apt-get update \
  && apt-get install --yes --no-install-recommends protobuf-compiler \
  && rm -rf /var/lib/apt/lists/* \
  && rustup set profile minimal \
  && rustup component add rustfmt clippy \
  && rustup toolchain install nightly --profile minimal \
  && cargo install cargo-audit --version 0.22.0 --locked --features fix

WORKDIR /workspace
ENTRYPOINT ["cargo"]
CMD ["--help"]
