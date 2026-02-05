FROM --platform=$BUILDPLATFORM golang:1.25

ARG GOLANGCI_LINT_VERSION=v1.64.5
ARG OAPI_CODEGEN_VERSION=v2.4.1
ARG TAILWIND_VERSION=v4.1.18
ARG GOFUMPT_VERSION=v0.7.0
ARG TEMPL_VERSION=v0.3.977
ARG BUF_VERSION=v1.50.0

ENV GOBIN=/usr/local/bin \
    PATH=/usr/local/go/bin:/usr/local/bin:/usr/bin:/bin

RUN apt-get update && apt-get install -y --no-install-recommends \
      ca-certificates git curl \
    && rm -rf /var/lib/apt/lists/*

RUN set -eux; \
  go install github.com/golangci/golangci-lint/cmd/golangci-lint@"${GOLANGCI_LINT_VERSION}"; \
  \
  go install mvdan.cc/gofumpt@"${GOFUMPT_VERSION}"; \
  \
  go install github.com/oapi-codegen/oapi-codegen/v2/cmd/oapi-codegen@"${OAPI_CODEGEN_VERSION}"; \
  \
  go install github.com/a-h/templ/cmd/templ@"${TEMPL_VERSION}"; \
  \
  arch="$(uname -m)"; \
  case "$arch" in \
    x86_64) buf_arch="x86_64" ;; \
    aarch64|arm64) buf_arch="aarch64" ;; \
    *) echo "unsupported arch: $arch" >&2; exit 1 ;; \
  esac; \
  curl -sSfL "https://github.com/bufbuild/buf/releases/download/${BUF_VERSION}/buf-Linux-${buf_arch}" \
    -o /usr/local/bin/buf; \
  chmod +x /usr/local/bin/buf; \
  curl -sSfL "https://github.com/tailwindlabs/tailwindcss/releases/download/${TAILWIND_VERSION}/tailwindcss-linux-${tw_arch}" \
      -o /usr/local/bin/tailwindcss; \
  chmod +x /usr/local/bin/tailwindcss; \
  \
  golangci-lint --version; \
  gofumpt -version || true; \
  oapi-codegen -version; \
  templ version; \
  buf --version

WORKDIR /workspace