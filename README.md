[![Apache 2.0](https://img.shields.io/badge/license-Apache2.0-orange.svg)](./LICENSE)

# Container Images

CI images used by Solti repositories.

## Model

<p align="center">
  <img src="https://raw.githubusercontent.com/soltiHQ/.github/main/assets/schema/solti-images-contract.svg" alt="Solti image contract: a Dockerfile defines image behavior, variants.yaml defines tags and build arguments, and a changed contract is built and published to GHCR" width="556">
</p>

## Contract

```text
ci/<toolchain>/
├── Dockerfile
└── variants.yaml
```

| Contract    | Registry image                     |
|-------------|------------------------------------|
| `ci/rust`   | `ghcr.io/soltihq/ci/rust`          |
| `ci/golang` | `ghcr.io/soltihq/ci/golang`        |
| `ci/proto`  | `ghcr.io/soltihq/ci/proto`         |

Each variant publishes one toolchain version tag.
The same build also publishes `<version>-sha-<commit>` for rollback and diagnostics.

Version tags are updated when their image contract changes.
Consumers pin the toolchain version and refresh it in CI.

The workflow does not publish `latest`.

## Contributing

Issues and pull requests are welcome.
Read the [contributing guide](https://github.com/soltiHQ/.github/blob/main/CONTRIBUTING.md) before a large change.

<br>

<p align="center">
  <a href="https://github.com/soltiHQ">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/soltiHQ/.github/main/assets/word/solti-word-light.svg">
      <img src="https://raw.githubusercontent.com/soltiHQ/.github/main/assets/logo/solti-logo-dark.svg" alt="soltiHQ" height="84">
    </picture>
  </a>
</p>
