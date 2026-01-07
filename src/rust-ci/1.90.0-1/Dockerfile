ARG RUST_VERSION=1.90.0

FROM --platform=$BUILDPLATFORM rust:${RUST_VERSION}-slim

RUN rustup set profile minimal \
  && rustup component add rustfmt clippy \
  && cargo install cargo-audit --version 0.22.0 --locked --features fix

WORKDIR /workspace
ENTRYPOINT ["cargo"]
CMD ["--help"]