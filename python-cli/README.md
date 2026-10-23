# Python CLI 模板

用于生成 Python 命令行项目，包含以下基础配置：

- 使用 `uv` 管理 Python 环境和项目依赖。
- 使用 `pytest` 编写和运行测试。
- 使用 Ruff 进行代码检查与格式化。
- 采用 `src/` 包布局。
- 可选使用 VS Code Dev Containers。
- 使用 GitHub Actions 自动执行 CI 检查。
- 提供 `AGENTS.md`，让 Codex 等 AI 编码助手遵循项目约定。

## 生成项目

建议所有仓库统一放在 `~/code`。在 macOS / Linux / WSL2 中：

```bash
mkdir -p ~/code
cd ~/code
git clone https://github.com/asher-tian/dev-templates.git
copier copy ./dev-templates/python-cli ./my-cli
```

如果模板仓库已存在于 `~/code/dev-templates`，跳过 clone 即可。Windows PowerShell 原生环境请使用 `$HOME\code` 下的目录；WSL2 开发则使用 WSL2 内部的 `~/code`。

Copier 会交互式询问项目名称、Python 包名和 Python 版本。

## 初始化与检查

```bash
cd ~/code/my-cli
uv sync --all-groups
uv run pytest
uv run ruff check .
uv run ruff format --check .
```

模板会生成 `.python-version`，供 uv 在本机选择对应 Python 版本；Dev Container 和 GitHub Actions 也使用所选版本。

## Dev Container

在 VS Code 中打开项目，然后执行 **Dev Containers: Reopen in Container**。容器会按项目配置安装 Python 和 uv，再运行 `uv sync --all-groups`。

`AGENTS.md` 提供项目级协作规范，但不会自动安装 Codex 或 Claude Code CLI，也不会把个人认证信息写入容器。若要在容器中运行 AI CLI，应在对应环境单独安装并按官方流程登录。
