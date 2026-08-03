# check=skip=InvalidDefaultArgInFrom
ARG BASE_IMAGE
FROM ${BASE_IMAGE}

ARG BUF_VERSION
ARG GOFUMPT_VERSION
ARG GOLANGCI_LINT_VERSION
ARG GOVULNCHECK_VERSION
ARG OAPI_CODEGEN_VERSION
ARG TAILWIND_VERSION
ARG TEMPL_VERSION
ARG TARGETARCH

ENV GOBIN=/usr/local/bin \
    PATH=/usr/local/go/bin:/usr/local/bin:/usr/bin:/bin

RUN apt-get update && apt-get install -y --no-install-recommends \
      ca-certificates git curl \
    && rm -rf /var/lib/apt/lists/*

RUN set -eux; \
  go install github.com/golangci/golangci-lint/cmd/golangci-lint@"${GOLANGCI_LINT_VERSION}"; \
  go install mvdan.cc/gofumpt@"${GOFUMPT_VERSION}"; \
  go install github.com/oapi-codegen/oapi-codegen/v2/cmd/oapi-codegen@"${OAPI_CODEGEN_VERSION}"; \
  go install github.com/a-h/templ/cmd/templ@"${TEMPL_VERSION}"; \
  go install golang.org/x/vuln/cmd/govulncheck@"${GOVULNCHECK_VERSION}"; \
  \
  case "${TARGETARCH}" in \
    amd64) buf_arch="x86_64"; tw_arch="x64" ;; \
    arm64) buf_arch="aarch64"; tw_arch="arm64" ;; \
    *) echo "unsupported arch: ${TARGETARCH}" >&2; exit 1 ;; \
  esac; \
  \
  curl -sSfL "https://github.com/bufbuild/buf/releases/download/${BUF_VERSION}/buf-Linux-${buf_arch}" \
    -o /usr/local/bin/buf; \
  chmod +x /usr/local/bin/buf; \
  \
  curl -sSfL "https://github.com/tailwindlabs/tailwindcss/releases/download/${TAILWIND_VERSION}/tailwindcss-linux-${tw_arch}" \
    -o /usr/local/bin/tailwindcss; \
  chmod +x /usr/local/bin/tailwindcss

WORKDIR /workspace
