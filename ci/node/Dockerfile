# check=skip=InvalidDefaultArgInFrom
ARG BASE_IMAGE
FROM ${BASE_IMAGE}

ARG NODE_VERSION

RUN apt-get update \
  && apt-get install --yes --no-install-recommends ca-certificates git \
  && rm -rf /var/lib/apt/lists/* \
  && test "$(node --version)" = "v${NODE_VERSION}"

ENV NPM_CONFIG_UPDATE_NOTIFIER=false

WORKDIR /workspace
