# geonet-open-data-viewer

A single-page, no-build web viewer for the public **GeoNet Open Data** S3 bucket
(`s3://geonet-open-data`, `ap-southeast-2`). Browse the datasets in your browser
and copy ready-to-run AWS CLI commands for anything you want to download.

[![CI - Validate and Test](https://github.com/jajera/geonet-open-data-viewer/actions/workflows/ci.yml/badge.svg)](https://github.com/jajera/geonet-open-data-viewer/actions/workflows/ci.yml)
[![Deploy to GitHub Pages](https://github.com/jajera/geonet-open-data-viewer/actions/workflows/pages.yml/badge.svg)](https://github.com/jajera/geonet-open-data-viewer/actions/workflows/pages.yml)
[![Markdown Lint](https://github.com/jajera/geonet-open-data-viewer/actions/workflows/markdown-lint.yml/badge.svg)](https://github.com/jajera/geonet-open-data-viewer/actions/workflows/markdown-lint.yml)
[![Commit Message Conformance](https://github.com/jajera/geonet-open-data-viewer/actions/workflows/commitmsg-conform.yml/badge.svg)](https://github.com/jajera/geonet-open-data-viewer/actions/workflows/commitmsg-conform.yml)

**Live app**: <https://jajera.github.io/geonet-open-data-viewer/>

## Overview

The bucket is part of the [AWS Open Data Sponsorship Program](https://registry.opendata.aws/geonet/),
so it is world-readable with no AWS account required. It also returns permissive
CORS headers, which lets a static page list its contents directly from the browser
using the S3 `ListObjectsV2` REST API — no backend, no credentials, no build step.

## Features

- **Browse folders and files** straight from S3, with breadcrumbs and deep links (`#/prefix`).
- **Sortable columns** — name, size, and last-modified (folders pinned on top).
- **Pagination** — page-size selector plus a "Load more" button (S3 continuation tokens).
- **Learn the AWS CLI** — a collapsible install guide (macOS, Windows, Linux) and
  copyable commands for every folder (`aws s3 ls` / `aws s3 sync`) and every file
  (`aws s3 cp ... --no-sign-request`, `curl`, and the raw URL).
- **Dark / light theme** that defaults to your system preference and remembers your choice.
- **Resilient** — in-flight guard and inline error/retry handling on network hiccups.

## Usage

Open the live app, browse into a dataset, and either click a file's **get** button
for its exact download command, or copy the folder-level commands. For example:

```bash
# list a folder (cheap, non-recursive)
aws s3 ls s3://geonet-open-data/waveforms/ --no-sign-request

# download a single object
aws s3 cp s3://geonet-open-data/<key> . --no-sign-request

# sync a specific folder
aws s3 sync s3://geonet-open-data/<prefix> ./local-dir --no-sign-request
```

Please download only what you need and keep local copies rather than re-syncing.

## Deployment

Pushes to `main` run the CI workflow; on success, the reusable
`actionsforge/actions/.github/workflows/github-pages-deploy.yml` publishes the
`docs/` directory to GitHub Pages.

## Data source and attribution

GeoNet data are made available free of charge under the
[CC BY 3.0 NZ licence](https://creativecommons.org/licenses/by/3.0/nz/). Please
acknowledge the GeoNet programme and its sponsors when using the data — see the
[GeoNet Data Policy](https://www.geonet.org.nz/policy). This project is an
independent viewer and is not affiliated with GeoNet.

## License

[MIT](LICENSE) © John Ajera
