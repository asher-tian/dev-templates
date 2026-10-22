# AI 编码助手协作规范

## 项目约定

- 使用 `uv` 管理 Python 环境和项目依赖，不要将项目依赖安装到全局 Python 环境。
- 运行时依赖放在 `[project].dependencies`，开发工具放在 `dev` 依赖组。
- 保持 `src/` 包布局。
- 保持 `pyproject.toml` 与 `uv.lock` 一致，并将两者提交到 Git。
- 只有在确有必要时才添加依赖；添加时说明原因。
- 不要提交 `.env` 文件、访问令牌、密码、私钥或其他敏感信息。

## 完成修改前

运行以下检查：

```bash
uv run ruff check .
uv run ruff format --check .
uv run pytest
```

如果某项检查无法执行，请明确说明原因，不要声称检查已通过。
