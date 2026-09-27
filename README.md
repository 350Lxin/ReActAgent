# ReActAgent

一个基于 Python 和 OpenRouter 的简单 ReAct Agent。Agent 会根据任务在“思考、调用工具、观察结果”之间循环，直到生成最终答案。

## 功能

- 使用 OpenRouter 兼容的 Chat Completions API
- 支持通过工具函数扩展 Agent 能力
- 自动生成工具列表和项目文件列表
- 支持执行终端命令等工具
- 使用 `uv` 管理 Python 环境和依赖

## 环境要求

- Python 3.14 或更高版本
- [uv](https://docs.astral.sh/uv/)
- OpenRouter API Key

## 安装

在项目目录执行：

```powershell
uv sync
```

## 配置 API Key

在项目根目录创建 `.env` 文件：

```env
OPENROUTER_API_KEY=你的OpenRouter_API_Key
```

不要将 `.env` 提交到 GitHub。项目已经通过 `.gitignore` 排除该文件。

## 运行

```powershell
uv run agent.py snake
```

启动后输入任务，例如：

```text
请输入任务：写一个贪吃蛇小游戏
```

其中 `snake` 是项目工作目录，Agent 会读取该目录中的文件，并根据模型输出调用工具。

## ReAct 输出格式

模型需要按以下格式返回内容：

```text
<thought>分析当前任务</thought>
<action>工具名(参数)</action>
```

完成任务后返回：

```text
<final_answer>最终答案</final_answer>
```

## 项目结构

```text
ReActAgent/
├── agent.py             # Agent 主程序和工具调用循环
├── prompt_template.py   # 系统提示词模板
├── pyproject.toml       # 项目配置和依赖
├── uv.lock              # 锁定依赖版本
└── src/reactagent/      # Python 包入口
```

## 安全提示

- 不要把 API Key 写入源代码。
- 不要将 `.env`、虚拟环境或缓存目录提交到仓库。
- 执行终端命令前应检查模型生成的命令，避免误删或覆盖文件。
