# dev-templates

用于个人开发的可复用项目模板仓库，使用 [Copier](https://copier.readthedocs.io/) 生成项目。

## 模板列表

- [python-cli](./python-cli/)：Python 命令行项目模板，包含 `uv`、`pytest`、Ruff、`src/` 包布局、可选的 VS Code Dev Containers，以及 GitHub Actions CI。

## 统一项目目录

新项目统一放在 `~/code` 下。macOS / Linux / WSL2：

```bash
mkdir -p ~/code
cd ~/code
```

Windows PowerShell 原生环境使用：

```powershell
New-Item -ItemType Directory -Force "$HOME\code" | Out-Null
Set-Location "$HOME\code"
```

Windows 原生的 `$HOME\code` 与 WSL2 内的 `~/code` 是两个不同位置。使用 WSL2 + Dev Containers 开发时，建议将项目保存在 WSL2 的 Linux 文件系统内。

## 生成项目

在 `~/code` 下克隆模板仓库，再指定模板子目录：

```bash
git clone https://github.com/asher-tian/dev-templates.git
copier copy ./dev-templates/python-cli ./my-cli
```

如果 `dev-templates` 已经克隆到 `~/code/dev-templates`，跳过 clone，直接执行 Copier 命令即可。Windows PowerShell 可使用相同命令和对应的相对路径。

Copier 会交互式询问项目名称、Python 包名和 Python 版本。

生成后进入项目目录，执行检查：

```bash
cd ~/code/my-cli
uv sync --all-groups
uv run pytest
uv run ruff check .
uv run ruff format --check .
```

## 模板维护原则

- 模板保持精简，只包含该类型项目真正需要的配置。
- 只有确实需要时，才添加 Redis、PostgreSQL 等基础设施。
- 项目依赖由 `uv` 管理，并提交 `pyproject.toml` 和 `uv.lock`。
- 项目环境配置与源代码一起提交，便于在不同电脑上重建开发环境。
- `AGENTS.md` 维护项目级 AI 协作规则；个人账号和认证信息不进入模板。
