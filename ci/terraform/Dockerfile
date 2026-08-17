# check=skip=InvalidDefaultArgInFrom
ARG BASE_IMAGE
FROM ${BASE_IMAGE}

ARG TARGETARCH
ARG TERRAFORM_VERSION

RUN set -eux; \
  apt-get update; \
  apt-get install --yes --no-install-recommends \
    bash ca-certificates curl git gnupg unzip; \
  case "${TARGETARCH}" in \
    amd64) terraform_arch="amd64" ;; \
    arm64) terraform_arch="arm64" ;; \
    *) echo "unsupported arch: ${TARGETARCH}" >&2; exit 1 ;; \
  esac; \
  curl -fsSL \
    "https://www.hashicorp.com/.well-known/pgp-key.txt" \
    -o /tmp/hashicorp-release-key.asc; \
  export GNUPGHOME=/tmp/gnupg; \
  mkdir -m 700 "${GNUPGHOME}"; \
  hashicorp_fingerprint=$( \
    gpg --batch --with-colons --import-options show-only \
      --import /tmp/hashicorp-release-key.asc \
      | awk -F: '$1 == "fpr" { print $10; exit }' \
  ); \
  test "${hashicorp_fingerprint}" = \
    "C874011F0AB405110D02105534365D9472D7468F"; \
  gpg --batch --import /tmp/hashicorp-release-key.asc; \
  gpg --batch --export > /tmp/release-keyring.gpg; \
  test -s /tmp/release-keyring.gpg; \
  terraform_base="https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}"; \
  terraform_zip="terraform_${TERRAFORM_VERSION}_linux_${terraform_arch}.zip"; \
  terraform_sums="terraform_${TERRAFORM_VERSION}_SHA256SUMS"; \
  terraform_signature="${terraform_sums}.72D7468F.sig"; \
  curl -fsSLO "${terraform_base}/${terraform_zip}"; \
  curl -fsSLO "${terraform_base}/${terraform_sums}"; \
  curl -fsSLO "${terraform_base}/${terraform_signature}"; \
  gpgv --keyring /tmp/release-keyring.gpg \
    "${terraform_signature}" "${terraform_sums}"; \
  grep " ${terraform_zip}$" "${terraform_sums}" | sha256sum -c -; \
  unzip "${terraform_zip}" -d /usr/local/bin; \
  rm "${terraform_zip}" "${terraform_sums}" "${terraform_signature}"; \
  rm -rf "${GNUPGHOME}" /tmp/hashicorp-release-key.asc \
    /tmp/release-keyring.gpg; \
  test "$(terraform version | sed -n 's/^Terraform v//p')" = \
    "${TERRAFORM_VERSION}"; \
  apt-get purge --yes --auto-remove gnupg; \
  rm -rf /var/lib/apt/lists/*

WORKDIR /workspace
