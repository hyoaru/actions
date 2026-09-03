# Hardened Actions

A personal collection of hardened GitHub Actions for personal usage. Each action wraps its official counterpart, pinned to a specific commit SHA for supply chain security.

## Overview

Tags are mutable and can be moved to malicious code at any time. Commit SHAs are immutable. Once pinned to a hash, that code can never change.

```
# Instead of this (mutable, unsafe):
- uses: actions/checkout@v4

# Use this (immutable, safe):
- uses: hyoaru/actions/checkout@main
```

## Available Actions

| Action                                    | SHA       | Upstream                                                                         |
| ----------------------------------------- | --------- | -------------------------------------------------------------------------------- |
| [`checkout`](checkout/)                   | `3d3c42e` | [actions/checkout](https://github.com/actions/checkout) v7.0.1                   |
| [`setup-node`](setup-node/)               | `8207627` | [actions/setup-node](https://github.com/actions/setup-node) v7.0.0               |
| [`upload-artifact`](upload-artifact/)     | `043fb46` | [actions/upload-artifact](https://github.com/actions/upload-artifact) v7.0.1     |
| [`download-artifact`](download-artifact/) | `3e5f45b` | [actions/download-artifact](https://github.com/actions/download-artifact) v8.0.1 |

## Usage

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: hyoaru/actions/checkout@v1

      - uses: hyoaru/actions/setup-node@v1
        with:
          node-version: 20
          cache: "npm"

      - run: npm ci
      - run: npm test

      - uses: hyoaru/actions/upload-artifact@v1
        with:
          name: build-output
          path: dist/
```

## Updating

Each action's `action.yml` contains the upstream SHA with a version comment:

```yaml
uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1 # v7.0.1
```

To update, change the SHA and version comment to the latest release.
