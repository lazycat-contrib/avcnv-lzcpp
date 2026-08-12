# avcnv-lzcpp

This repository packages `evilhsu/avcnv:latest` as a LazyCat LPK v2 application.

## Runtime

- Package ID: `cloud.lazycat.app.media-converter`
- Version: `1.0.0`
- Manifest runtime image: `docker.1ms.run/evilhsu/avcnv:latest`
- Upstream image source for automation: `docker.io/evilhsu/avcnv`
- HTTP entrypoint: `/` -> `http://avcnv:5123/`
- Persistent data:
  - `/lzcapp/var/uploads` -> `/app/uploads`
  - `/lzcapp/var/localfiles` -> `/app/localfiles`
  - `/lzcapp/var/outputs` -> `/app/outputs`

## Build

This project now uses LPK v2 metadata split across `package.yml`, `lzc-manifest.yml`, and `lzc-build.yml`, with `min_os_version: 1.5.0`.

## Automation

`.github/lazycat-action.yml` tracks the mutable upstream tag through mirror mode using the built-in Docker Hub mirror path. The configuration keeps the upstream source on `docker.io/evilhsu/avcnv`, requires digest matching, and publishes only to the MiaoMiao private store.

`.github/workflows/lazycat.yml` supports:

- `push` on `main`
- `workflow_dispatch`
- reusable `workflow_call`

It produces versioned GitHub Release assets named like `cloud.lazycat.app.media-converter-v1.0.0.lpk`.

Required GitHub Secrets:

- `LZC_API_TOKEN`
- `APPSTORE_URL`
- `APPSTORE_TOKEN`
- `APP_ID` (optional)
- `PRIVATE_STORE_GROUP_CODES` (optional)
