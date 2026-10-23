# AI 编码助手协作规范

## 项目结构与环境

- 这是一个 Python CLI 项目，应用代码放在 `src/`，测试放在 `tests/`。
- 使用 `uv` 管理 Python 解释器、虚拟环境和依赖；不要将项目依赖安装到全局 Python 环境。
- `.python-version` 用于本机选择 Python 版本；`pyproject.toml`、Dev Container 和 CI 的 Python 版本应保持一致。修改版本时检查这些配置是否需要一起更新。
- 运行时依赖放在 `pyproject.toml` 的 `[project].dependencies`，开发工具放在 `[dependency-groups].dev`。
- 保持 `src/` 包布局。
- 保持 `pyproject.toml` 与 `uv.lock` 一致，并将两者提交到 Git。
- 只有在确有必要时才添加依赖；添加时说明原因。

## 常用命令

```bash
uv sync --all-groups
uv run pytest
uv run ruff check .
uv run ruff format --check .
```

CLI 入口、运行方式和项目特定命令以 `README.md` 与 `pyproject.toml` 为准。优先使用 `uv run` 执行项目工具，避免依赖未记录的全局安装。

## Dev Container

- 优先使用仓库中的 `.devcontainer/` 配置复现 Linux 开发环境。
- 环境变更应更新 Dockerfile、Dev Container 配置或依赖文件，不要只在运行中的容器里手工安装后就结束。
- 代码和 Git 历史属于工作区；不要把源代码复制进镜像，也不要把个人认证目录烘焙进镜像。
- Codex / Claude Code CLI 是否安装在容器内由项目维护者决定。不要假设宿主机 CLI 或登录状态会自动出现在容器里。

## 安全约定

- 不要提交 `.env` 文件、访问令牌、密码、私钥或其他敏感信息。
- 不要为图方便挂载整个宿主机用户目录。
- 不要在未执行检查时声称测试通过。

## 完成修改前

运行以下检查：

```bash
uv run ruff check .
uv run ruff format --check .
uv run pytest
```

如果某项检查无法执行，请明确说明原因，不要声称检查已通过。
