# dev-templates

用于个人开发的可复用项目模板仓库，使用 [Copier](https://copier.readthedocs.io/) 生成项目。

## 内容导航

- [Git 配置指南](./git-config/README.md)：配置 GitHub / Gitee SSH、GitHub Verified 签名提交，以及双平台同步。

## 模板列表

- [python-cli](./python-cli/)：Python 命令行项目模板，包含 `uv`、`pytest`、Ruff、`src/` 包布局、可选的 VS Code Dev Containers，以及 GitHub Actions CI。

## Copier 官方资料

- [Copier 官方文档](https://copier.readthedocs.io/)
- [Copier 官方 GitHub 仓库](https://github.com/copier-org/copier)

## 生成项目

当前仓库包含多个模板目录，因此先克隆仓库，再将模板子目录作为本地模板路径传给 Copier：

```bash
git clone https://github.com/asher-tian/dev-templates.git
copier copy ./dev-templates/python-cli ./my-cli
```

如果仓库已经克隆到其他位置，将命令中的 `./dev-templates/python-cli` 替换为实际路径即可。

Copier 会交互式询问项目名称、Python 包名和 Python 版本。

生成后进入项目目录，执行检查：

```bash
cd my-cli
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
