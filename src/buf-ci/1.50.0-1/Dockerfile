FROM debian:bookworm-slim

ARG BUF_VERSION=v1.50.0
ARG TARGETARCH

RUN apt-get update && apt-get install -y --no-install-recommends \
      ca-certificates git curl \
    && rm -rf /var/lib/apt/lists/*

RUN set -eux; \
  case "${TARGETARCH}" in \
    amd64) buf_arch="x86_64" ;; \
    arm64) buf_arch="aarch64" ;; \
    *) echo "unsupported arch: ${TARGETARCH}" >&2; exit 1 ;; \
  esac; \
  curl -sSfL "https://github.com/bufbuild/buf/releases/download/${BUF_VERSION}/buf-Linux-${buf_arch}" \
    -o /usr/local/bin/buf; \
  chmod +x /usr/local/bin/buf; \
  buf --version

WORKDIR /workspace
