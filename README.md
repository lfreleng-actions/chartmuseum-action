<!--
# SPDX-License-Identifier: Apache-2.0
# SPDX-FileCopyrightText: 2025 The Linux Foundation
-->

# ☸️ ChartMuseum Container

Starts and runs a ChartMuseum Helm Chart repository/docker container with
**Docker layer caching** for optimal performance in CI/CD pipelines.

## Features

- 🚀 **50-80% faster** follow-up runs with intelligent Docker caching
- 🐳 **Docker layer caching** for ChartMuseum container images
- ⚙️ **Configurable caching** with custom key suffixes
- 🔄 **Cross-workflow cache sharing** within repositories
- 📦 **Production-ready** with backward compatibility

## Quick Start

<!-- markdownlint-disable MD046 -->

```yaml
steps:
  - name: "Run ChartMuseum with optimal caching"
    uses: lfreleng-actions/chartmuseum-action@main
    with:
      password: ${{ secrets.github_token }}
      port: 8080
      script: 'job.sh'
      # Caching enabled by default for best performance
```

<!-- markdownlint-enable MD046 -->

## Performance & Caching Architecture

This action includes Docker layer caching to speed up container
builds and follow-up runs:

### Docker Layer Caching

- **Caches Docker layers** from the ChartMuseum container image
- **Pre-pulls container images** for faster startup times
- **Preserves layers** between workflow runs
- **Smart cache keys** based on OS, version, and optional suffix

### Performance Benefits

- **First run**: Downloads and caches all necessary Docker images
- **Follow-up runs**: Leverages cached layers for **50-80% faster** startup
- **Cross-workflow sharing**: Cache works across workflows in same repo
- **Reduced resource usage**: Lower bandwidth and GitHub Actions minutes

### Caching Configuration Examples

**Basic usage (caching enabled by default):**

```yaml
- name: "Run ChartMuseum"
  uses: lfreleng-actions/chartmuseum-action@main
  with:
    password: ${{ secrets.github_token }}
    port: 8080
    script: 'job.sh'
```

**Custom cache isolation:**

```yaml
- name: "Run ChartMuseum with cache isolation"
  uses: lfreleng-actions/chartmuseum-action@main
  with:
    password: ${{ secrets.github_token }}
    port: 8080
    script: 'job.sh'
    cache_key_suffix: '-production'
```

**Disable caching (not recommended):**

```yaml
- name: "Run ChartMuseum without caching"
  uses: lfreleng-actions/chartmuseum-action@main
  with:
    password: ${{ secrets.github_token }}
    port: 8080
    script: 'job.sh'
    enable_cache: false
```

## Inputs

<!-- markdownlint-disable MD013 -->

| Name             | Required | Default     | Description                                                |
| ---------------- | -------- | ----------- | ---------------------------------------------------------- |
| password         | True     |             | Password to access ChartMuseum service                     |
| username         | False    | chartmuseum | Username to access ChartMuseum service                     |
| port             | False    | 8080        | TCP port on which server will listen                       |
| directory        | False    | charts      | Directory path to host Helm Charts                         |
| script           | False    |             | Path to shell script containing chart publishing steps     |
| exec_time        | False    | 120         | Background container/service execution time                |
| version          | False    | v0.16.3     | ghcr.io/helm/chartmuseum container version                 |
| purge_charts     | False    | false       | Purges any previous charts content at server startup       |
| exit             | False    | true        | Terminates the background container when the job completes |
| debug            | False    | false       | Enables Docker container debugging                         |
| enable_cache     | False    | true        | Enable Docker layer caching for faster builds              |
| cache_key_suffix | False    |             | Extra suffix for cache keys to allow cache isolation       |

<!-- markdownlint-enable MD013 -->

## Outputs

<!-- markdownlint-disable MD013 -->

| Name | Description                                 |
| ---- | ------------------------------------------- |
| cid  | Container ID of running Chartmuseum service |

<!-- markdownlint-enable MD013 -->

## Implementation Details

Uses the Docker container:

[ghcr.io/helm/chartmuseum](https://github.com/helm/chartmuseum/pkgs/container/chartmuseum)
