ARG RUST_VERSION=1.90.0
ARG CARGO_AUDIT_VERSION=0.22.0

FROM --platform=$BUILDPLATFORM rust:${RUST_VERSION}-slim

RUN rustup set profile minimal \
  && rustup component add rustfmt clippy \
  && cargo install cargo-audit --version ${CARGO_AUDIT_VERSION} --locked --features fix

WORKDIR /workspace

ENTRYPOINT ["cargo"]
CMD ["--help"]