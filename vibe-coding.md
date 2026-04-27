# AI编程

## 技术演进路径

核心能力与范式转变

1. 辅助编程：根据上下文提供代码建议或补全，提升单点编码效率，代表：GitHub Copilot，
2. 对话编程:  开发者通过自然语言进行对话交互，代表：ChatGPT
3. Agent编程：AI智能体能够自主完成从需求理解、任务规划、代码编写、调试、测试到部署的全流程闭环工作。催生Vibe Coding等新范式

## 主流工具

### 全形态全流程派

- 代表：腾讯云CodeBunny、阿里通义CodeMind

### AI原生IDE派

- 代表：Cursor、Trae

### 插件生态派

- 代表：GitHub Copilot、通义灵码、JetBrains AI

### 命令行智能体派

- 代表：Claude Code、Qwen Code

### 开源框架派

- 代表： OpenCode、Codex CLI

## 主流 CLI AI 编程工具

| 工具          | 优点                                 | 缺点                     | 底座模型           |
| :-------------- | :------------------------------------- | :------------------------- | :------------------- |
| Claude Code   | 代码理解深、终端自动化强、生成质量高 | 响应慢、模型单一、成本高 | Claude Sonnet/Opus |
| Codex CLI     | 自主工作能力强、动态思考、代码审查强 | 社区口碑待提升、成本高   | GPT-5-Codex        |
| Gemini CLI    | 成本极低、上下文超长、多模态         | 终端自动化深度相对较弱   | Gemini 2.5/3.1 Pro |
| Kimi Code CLI | 中文上下文超长、中文友好、国内直连   | 仅支持Kimi模型           | Kimi K2.5          |
| Qwen Code     | 上下文超长、智能体能力强、多模态     | 市场认知度待提升         | Qwen3.6-Plus       |
| OpenCode      | 模型完全自由、开源免费               | 能力依赖用户自选模型     | 用户自选           |

## AI开源社区

[魔搭社区 ](https://modelscope.cn/home)(ModelScope)

#### 大模型厂商开放平台

1. [深度求索DeepSeek](https://api-docs.deepseek.com/zh-cn/)
2. [智普GLM](https://docs.bigmodel.cn/cn/guide/start/introduction)
3. [月之暗面Kimi](https://platform.kimi.com/docs/overview)
4. [MiniMax](https://platform.minimaxi.com/docs/guides/models-intro)

#### 大模型开发与应用平台

1. **[阿里云百炼](https://help.aliyun.com/zh/model-studio/what-is-model-studio)**
2. **[火山方舟](https://www.volcengine.com/docs/82379?lang=zh)**
3. **[百度千帆](https://cloud.baidu.com/doc/qianfan/s/rmh8khvwu)**

#### Token工厂

[硅基流动](https://docs.siliconflow.cn/cn/userguide/introduction)

# 调用云端大模型API

# 调用本地部署的大模型

# LSP(Language Server Protocol)语言服务器协议

微软在 2016 年提出并开源的一种**通信协议**
LSP 是一个标准化的 JSON-RPC 协议，将编译器/分析器的能力封装成独立的服务器进程，让任何编辑器都可以通过该协议获得一致的、深度的语言智能支持，从而终结了“每种语言需为每个编辑器写插件”的时代。

1. ​LSP Client（客户端）​：编辑器/IDE，负责与用户交互（显示代码、高亮、光标位置等），向服务器发送请求。
2. LSP Server（服务器）：后台进程，包含特定语言的“深度知识”（语法、AST、类型系统、依赖分析等），执行实际的代码分析任务。

# Function Calling函数调用

1. 提出：OpenAI, 2023.6
2. 作用：允许开发者定义函数接口，让模型能够结构化地输出函数名称和参数，从而实现了模型与外部世界的精准交互
3. 类比：电脑操作系统/ 机器人的肌肉和神经末梢
4. 演化：**Tool Calls工具调用**

# MCP(Model Context Protocol)模型上下文协议

[官方文档](https://mcp-docs.cn/docs/getting-started/intro)

[中文指南](https://mcpcn.com/docs/introduction/)

1. 提出：Anthropic, 2024.11
2. 作用：通过定义 Client-Server 架构和 JSON-RPC 交互规范，MCP 让 AI 模型能够以标准化的方式连接各种工具和数据（如本地文件、数据库、API），而无需为每个工具单独开发集成。（类似LSP）
3. 类比：USB-C接口/机器人的标准化关节和接口

## MCP架构

| 角色名称 | 英文术语 | 通俗比喻    | 具体职责                                                                                         |
| :--------- | :--------- | :------------ | :------------------------------------------------------------------------------------------------- |
| 宿主     | Host     | 顾客        | 你正在使用的 AI 软件（如 Claude Desktop、Cursor 编辑器）。它负责发起请求：“我要查数据”。       |
| 客户端   | Client   | 服务员      | 它是运行在 Host 里的一个组件。它听懂顾客的话，然后标准化地传达给后厨。                               |
| 服务器   | Server   | 后厨/资源方 | 具体的工具或数据源（如你的本地文件、高德地图 API、GitHub）。它接收指令，干活，然后把结果端上来。 |

## MCP Server 向 Host 声明能力

* **Resources（资源）**
* **Tools（工具）**
* **Prompts（提示模板）**
* **Sampling（采样）**

## AI工具(MCP Host+ MCP Client)

它其实是一个​**遵循 MCP 协议的智能路由微服务**​，内部包含一个 MCP 客户端。它只做三件事：

1. ​**向下（对 Server）**：充当协调中心，用 MCP 协议去发现、调用所有外部工具。
2. ​**向上（对 API）**：充当一个顶级的“演员”，把来自 MCP 世界的所有信息，完美地翻译成 API 世界里的 Function Calling 格式。
3. ​**对外（对你）**：提供一个统一的接口，让你只需要跟它对话，就能用到整个 MCP 生态的工具。

## MCP部署方式

### Local Mode本地部署

​客户端主进程启动服务端子进程，通过stdin/stdout管道通信。
适用场景：

1. 本地文件系统访问
2. 执行构建脚本
3. 运行测试用例
4. Git操作
5. 数据分析与隐私敏感任务
6. 边缘计算与低延迟场景

### Remote Mode远程部署

服务端部署在远程机器，通过HTTP/SSE与客户端通信

适用场景：

1. 企业/团队协作：集中管理，共享资源
2. 安全与权限敏感环境：OAuth等机制实现统一认证和审计

### 配置示例

1. [claude-code](https://code.claude.com/docs/zh-CN/mcp)
2. [opencode](https://opencode.ai/docs/zh-cn/mcp-servers/)

# Skill技能

1. 提出：Anthropic, 2025.10
2. 作用：Skill 被视为对 MCP 和 Function Calling 的进一步抽象和优化。它将多步业务流程、工具调用逻辑封装为可复用的“能力单元”
3. 类比：专业软件/封装好的复杂动作模块
