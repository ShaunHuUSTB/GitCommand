# UV

一个用 Rust 编写的"全能型"Python管理工具：pip + virtualenv + pyenv + poetry 合体版

[官方文档](https://hellowac.github.io/uv-zh-cn/)

## 安装

```bash
# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## 常用命令

| 你要做的事 | uv 命令 | 以前要干什么 |
| :--- | :--- | :--- |
| 新建项目 | `uv init my_project` | 手动 `mkdir` + `python -m venv` + 创建配置文件 |
| 安装依赖 | `uv add requests` | `pip install requests` + 手动记到 requirements.txt |
| 运行代码 | `uv run python main.py` | 先激活虚拟环境，再 `python main.py` |

| 场景 | 命令 | 说明 |
| :--- | :--- | :--- |
| 安装特定 Python 版本 | `uv python install 3.12` | 没装的话自动下载 |
| 同步环境（团队协作） | `uv sync` | 根据 pyproject.toml 一键装好所有依赖 |
| 移除依赖 | `uv remove requests` | 自动更新配置文件 |
| 临时运行工具 | `uvx ruff check .` | 用完即走，不污染项目环境 |
