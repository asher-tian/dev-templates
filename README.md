# dev-templates

个人开发项目模板集合，使用 [Copier](https://copier.readthedocs.io/) 从模板生成新项目。

## 模板目录

| 模板 | 适用场景 | 说明 |
|---|---|---|
| [python-cli](./python-cli/) | Python 命令行应用 | uv、pytest、Ruff、src 布局、可选 Dev Container、GitHub Actions CI |

每个模板的具体参数、生成步骤、依赖安装和开发命令，请查看对应目录中的 README。

## 使用约定

- 所有项目仓库统一放在 `~/code` 下。
- Windows 原生环境使用 `$HOME\code`；Windows + WSL2 开发时，使用 WSL2 内部的 `~/code`。
- 项目语言版本、依赖锁文件、容器配置和 CI 应随项目一起维护，便于在不同电脑上复现。
- 模板只包含该类项目通用且确实需要的配置；Redis、数据库等服务按项目需要添加。
- 项目级 AI 协作规则放在生成项目的 `AGENTS.md` 等文件中；不要将个人账号、令牌、SSH 私钥或登录缓存写进模板。

## 新建项目

1. 选择上方合适的模板。
2. 阅读该模板目录中的 README。
3. 使用 Copier 生成项目，并按模板说明安装依赖、运行测试。

例如，Python CLI 模板的详细操作见 [python-cli/README.md](./python-cli/README.md)。

## 相关仓库

- [dev-env](https://github.com/asher-tian/dev-env)：新电脑初始化、Git / SSH、开发工具与终端配置。
