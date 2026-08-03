# check=skip=InvalidDefaultArgInFrom
ARG BASE_IMAGE
FROM ${BASE_IMAGE}

ARG CARGO_AUDIT_VERSION

RUN apt-get update \
  && apt-get install --yes --no-install-recommends protobuf-compiler \
  && rm -rf /var/lib/apt/lists/* \
  && rustup set profile minimal \
  && rustup component add rustfmt clippy \
  && rustup toolchain install nightly --profile minimal \
  && cargo install cargo-audit --version "${CARGO_AUDIT_VERSION}" --locked --features fix

WORKDIR /workspace
ENTRYPOINT ["cargo"]
CMD ["--help"]
