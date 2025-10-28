ARG RUST_VERSION

FROM --platform=$BUILDPLATFORM rust:${RUST_VERSION}-slim

RUN rustup set profile minimal \
 && rustup component add rustfmt clippy

WORKDIR /
ENTRYPOINT ["cargo"]
CMD ["--help"]