# Python CLI 模板

用于生成 Python 命令行项目，包含以下基础配置：

- 使用 `uv` 管理 Python 环境和项目依赖。
- 使用 `pytest` 编写和运行测试。
- 使用 Ruff 进行代码检查与格式化。
- 采用 `src/` 包布局。
- 可选使用 VS Code Dev Containers。
- 使用 GitHub Actions 自动执行 CI 检查。

## Copier 官方资料

- [Copier 官方文档](https://copier.readthedocs.io/)
- [Copier 官方 GitHub 仓库](https://github.com/copier-org/copier)

## 生成项目

```bash
copier copy gh:asher-tian/dev-templates/python-cli ./my-cli
```

Copier 会交互式询问项目名称、Python 包名和 Python 版本。

生成后执行：

```bash
cd my-cli
uv sync --all-groups
uv run pytest
uv run ruff check .
uv run ruff format --check .
```

这个模板有意保持精简。只有项目确实需要时，再添加 Redis、数据库或其他基础设施。
