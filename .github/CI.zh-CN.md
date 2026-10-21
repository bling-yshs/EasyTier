# CI

[English](CI.md)

仅保留 [EasyTier Build](workflows/build.yml) 一个 workflow。每次 push 和
pull request 都会触发，也可以在 GitHub Actions 页面手动运行。

`build` 任务使用 Ubuntu 24.04，通过现有的 `prepare-build` action 准备
Rust 工具链和原生编译工具，关闭 GUI 和前端环境准备，并缓存 Rust 编译产物。

编译命令为：

```sh
cargo build --locked --bins --package easytier --package easytier-web
```

该命令使用默认 feature 编译 `easytier-core`、`easytier-cli` 和
`easytier-web`。Web 服务不嵌入前端资源，编译过程中不允许修改锁文件。

CI 仅验证编译，不运行格式检查、lint 或测试，不构建 GUI/移动端安装包，
不上传产物、签名、发布版本或推送容器镜像。同一分支或 PR 的新任务会取消旧任务。
