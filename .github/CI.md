# CI

[中文](CI.zh-CN.md)

The only workflow is [EasyTier Build](workflows/build.yml). It runs on every
push and pull request, and can also be started manually from GitHub Actions.

The `build` job runs on Ubuntu 24.04. It uses the existing `prepare-build`
action to install the Rust toolchain and native build tools, with GUI and
frontend preparation disabled. Rust compilation outputs are cached.

The build command is:

```sh
cargo build --locked --bins --package easytier --package easytier-web
```

This compiles `easytier-core`, `easytier-cli`, and `easytier-web` with their
default features. The Web server is built without embedded frontend assets.
The lockfile must remain unchanged during the build.

CI only validates compilation. It does not run formatting, linting, or tests,
build GUI/mobile packages, upload artifacts, sign binaries, publish releases,
or push container images. A new run cancels an older run for the same branch
or pull request.
