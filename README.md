<!--
# SPDX-License-Identifier: Apache-2.0
# SPDX-FileCopyrightText: 2025 The Linux Foundation
-->

# ☸️ ChartMuseum Container

Starts and runs a ChartMuseum Helm Chart repository/docker container.

## chartmuseum-action

## Usage Example

<!-- markdownlint-disable MD046 -->

```yaml
steps:
  - name: "Run ChartMuseum"
    uses: lfreleng-actions/chartmuseum-action@main
    with:
      password: ${{ secrets.github_token }}
      port: 8080
      script: 'job.sh'
```

<!-- markdownlint-enable MD046 -->

## Inputs

<!-- markdownlint-disable MD013 -->

| Name         | Required | Default     | Description                                                |
| ------------ | -------- | ----------- | ---------------------------------------------------------- |
| password     | True     |             | Password to access ChartMuseum service                     |
| username     | False    | chartmuseum | Username to access ChartMuseum service                     |
| port         | False    | 8080        | TCP port on which server will listen                       |
| directory    | False    | charts      | Directory path to host Helm Charts                         |
| script       | False    |             | Path to shell script containing chart publishing steps     |
| exec_time    | False    | 120         | Background container/service execution time                |
| version      | False    | v0.16.3     | ghcr.io/helm/chartmuseum container version                 |
| purge_charts | False    | false       | Purges any previous charts content at server startup       |
| exit         | False    | true        | Terminates the background container when the job completes |
| debug        | False    | false       | Enables Docker container debugging                         |

<!-- markdownlint-enable MD013 -->

## Implementation Details

Uses the Docker container:

[ghcr.io/helm/chartmuseum](https://github.com/helm/chartmuseum/pkgs/container/chartmuseum)
