# UV

一个用 Rust 编写的"全能型"Python管理工具：pip + virtualenv + pyenv + poetry 合体版

[官方文档](https://hellowac.github.io/uv-zh-cn/)

## 安装

1. 命令安装
```bash
# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh
```

2. 手动安装
仓库下载zip包解压：https://github.com/astral-sh/uv/releases

## 配置

1. 全局配置文件路径环境变量
  UV_CONFIG_FILE = D:\Env\uv\config\uv.toml

2. 全局配置文件
| 环境变量 | `uv.toml` 配置键 | 说明 |
| :--- | :--- | :--- |
| `UV_CACHE_DIR` | `cache-dir` | 设置依赖包的缓存目录路径 |
| `UV_DEFAULT_INDEX` | `index-url` | 设置默认的 PyPI 镜像源 URL |
| `UV_INSECURE_HOST` | `allow-insecure-host` | 允许不安全的 HTTP 主机或忽略证书验证 |
| `UV_PYTHON_INSTALL_MIRROR` | `python-install-mirror` | 设置 Python 解释器安装的镜像源 |

```
cache-dir = "D:\\Env\\uv\\cache" 
index-url = "https://pypi.tuna.tsinghua.edu.cn/simple"
allow-insecure-host = ["pypi.example.org", "internal-pypi.local"]
python-install-mirror = "https://github.com/astral-sh/python-build-standalone/releases/download"
```

3. 全局环境变量
| 环境变量名 | 作用说明 | 默认值 (参考) | 迁移目录示例 (Windows) |
| :--- | :--- | :--- | :--- |
| `UV_INSTALL_DIR` | `uv` 自身的安装目录。<br>控制 `uv.exe` 二进制文件安装在哪里。 | `~/.local/bin`<br>(即用户目录下的 bin) | `D:\Env\uv\bin` |
| `UV_PYTHON_INSTALL_DIR` | Python 解释器的存储目录。<br>`uv` 下载和管理的 Python 版本（如 cpython-3.12）实体文件存放在这里。 | `~/.local/share/uv/python`<br>(即 AppData 下) | `D:\Env\uv\python` |
| `UV_PYTHON_BIN_DIR` | Python 可执行文件的软链接目录。<br>用于存放指向上述 Python 版本的快捷方式（如 `python.exe`），方便系统调用。 | `~/.local/bin` | `D:\Env\uv\bin` |
| `UV_TOOL_DIR` | 第三方工具的存储目录。<br>当你使用 `uv tool install` 时，工具的本体文件（虚拟环境）存放在这里。 | `~/.local/share/uv/tools` | `D:\Env\uv\tools` |
| `UV_TOOL_BIN_DIR` | 第三方工具的可执行文件目录。<br>工具的可执行文件（如 `ruff.exe`, `httpie.exe`）会链接到这里。 | `~/.local/bin` | `D:\Env\uv\bin` |
| `UV_INSTALLER_GITHUB_BASE_URL` | `uv` 自身更新的下载源。<br>用于 `uv self update` 命令，指定 GitHub 的基础 URL。 | `https://github.com` | *(此项为 URL 配置)*<br>例如：<br>`https://ghproxy.cn/https://github.com` |

## 基础版本管理

| 功能描述 | 命令示例 | 说明 |
| :--- | :--- | :--- |
| 列出可用版本 | `uv python list` | 显示本地已安装及可下载的 Python 版本<websource>source_group_web_2</websource>。 |
| 安装指定版本 | `uv python install 3.12` | 下载并安装 Python 3.12（支持具体版本号如 `3.12.1`）<websource>source_group_web_3</websource>。 |
| 查找版本路径 | `uv python find 3.11` | 显示指定版本 Python 解释器的绝对路径<websource>source_group_web_4</websource>。 |
| 固定项目版本 | `uv python pin 3.10` | 将当前项目锁定为使用 Python 3.10（生成 `.python-version` 文件）<websource>source_group_web_5</websource>。 |
| 卸载版本 | `uv python uninstall 3.9` | 从系统中移除指定的 Python 版本<websource>source_group_web_6</websource>。 |
| 查看安装目录 | `uv python dir` | 显示 `uv` 管理 Python 版本的存储目录路径<websource>source_group_web_7</websource>。 |

## 项目生命周期

| 功能描述 | 命令示例 | 说明 |
| :--- | :--- | :--- |
| 初始化项目 | `uv init my-project` | 创建一个新的项目目录，并自动生成 `pyproject.toml`、`README.md` 等基础文件<websource>source_group_web_2</websource>。 |
| 添加依赖 | `uv add requests` | 安装 `requests` 包，并自动将其添加到 `pyproject.toml` 和 `uv.lock` 文件中<websource>source_group_web_3</websource>。 |
| 添加开发依赖 | `uv add --dev pytest` | 安装仅用于开发的依赖（如测试、 linting 工具）<websource>source_group_web_4</websource>。 |
| 同步环境 | `uv sync` | 根据 `pyproject.toml` 和 `uv.lock` 文件，确保虚拟环境与项目依赖完全一致<websource>source_group_web_5</websource>。 |
| 运行项目命令 | `uv run python main.py` | 在项目虚拟环境中运行脚本，无需手动激活环境<websource>source_group_web_6</websource>。 |
| 移除依赖 | `uv remove requests` | 从项目中卸载并移除指定的依赖包<websource>source_group_web_7</websource>。 |

## 导出与构建

| 功能描述 | 命令示例 | 说明 |
| :--- | :--- | :--- |
| 导出依赖列表 | `uv export > requirements.txt` | 将项目依赖导出为标准的 `requirements.txt` 文件<websource>source_group_web_14</websource>。 |
| 导出开发依赖 | `uv export --dev > req-dev.txt` | 将项目依赖和开发依赖一同导出<websource>source_group_web_15</websource>。 |
| 构建项目包 | `uv build` | 根据项目配置构建可分发的包（如 wheel 和 sdist）<websource>source_group_web_16</websource>。 |
| 发布项目包 | `uv publish` | 将构建好的包发布到 PyPI 或其他包索引<websource>source_group_web_17</websource>。 |

