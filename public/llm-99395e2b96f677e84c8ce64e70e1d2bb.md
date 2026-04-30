# LLM 命令行工具使用指南

## 简介

[llm](https://llm.datasette.io/) 是一个命令行工具，用于统一调用各种大语言模型 API。

## 安装

推荐在虚拟环境中安装，以避免依赖冲突。

```bash
# 创建并激活虚拟环境（以 venv 为例）
python3 -m venv llm-env
source llm-env/bin/activate  # Linux/macOS
# llm-env\Scripts\activate  # Windows

# 安装 llm
pip install llm
```

## 配置

### 配置文件路径

`llm` 使用以下主要目录来管理配置和数据：

| 用途 | 路径 |
|------|------|
| 用户数据（密钥、日志） | `~/.config/io.datasette.llm/` |
| 模型配置文件 | `~/.config/io.datasette.llm/extra-openai-models.yaml` |

可通过环境变量 `LLM_USER_PATH` 自定义用户数据目录的位置。

### API Key 管理

使用 `llm` 自带的密钥管理功能，密钥保存在本地 `keys.json` 中：

```bash
# 交互式输入 API Key（不会暴露在 Shell 历史中）
llm keys set openai
```

#### `api_key_name` 与 `keys.json` 的映射关系

在模型配置文件中指定的 `api_key_name`，其值对应本地 `keys.json` 文件中的键名。例如，当 `api_key_name` 设置为 `openai` 时，`llm` 会从 `keys.json` 文件中查找键为 `"openai"` 的值作为 API 密钥。

**`keys.json` 示例**:

```json
{
  "// Note": "This file stores secret API credentials. Do not share!",
  "openai": "sk-你的真实API密钥",
  "anthropic": "sk-ant-你的密钥"
}
```

### 第三方模型配置（通过阿里云百炼调用）

对于非 OpenAI 原生模型（如千问、DeepSeek、GLM 等），可以通过配置 `extra-openai-models.yaml` 文件，将其添加到阿里云百炼（DashScope）的兼容端点中。

`extra-openai-models.yaml` 配置文件格式如下：

```yaml
# 配置示例：添加 qwen-turbo 模型
- model_id: qwen-turbo          # 在 llm 命令行中使用的模型标识符
  model_name: qwen-turbo        # 实际传递给 API 的模型名称
  api_base: "https://dashscope.aliyuncs.com/compatible-mode/v1"  # 阿里云百炼兼容端点
  api_key_name: openai          # 对应 keys.json 中的密钥名称
```

**常用模型配置示例**：

```yaml
# 千问系列
- model_id: qwen3-max
  model_name: qwen3-max
  api_base: "https://dashscope.aliyuncs.com/compatible-mode/v1"
  api_key_name: openai

- model_id: qwen3.6-plus
  model_name: qwen3.6-plus
  api_base: "https://dashscope.aliyuncs.com/compatible-mode/v1"
  api_key_name: openai

- model_id: qwen3.5-flash
  model_name: qwen3.5-flash
  api_base: "https://dashscope.aliyuncs.com/compatible-mode/v1"
  api_key_name: openai

# DeepSeek
- model_id: deepseek-v3.2
  model_name: deepseek-v3.2
  api_base: "https://dashscope.aliyuncs.com/compatible-mode/v1"
  api_key_name: openai

# GLM 智谱
- model_id: glm-5
  model_name: glm-5
  api_base: "https://dashscope.aliyuncs.com/compatible-mode/v1"
  api_key_name: openai

# Kimi
- model_id: kimi-k2.5
  model_name: kimi-k2.5
  api_base: "https://dashscope.aliyuncs.com/compatible-mode/v1"
  api_key_name: openai
```

> **注意**：模型列表可能随时间变化。最准确、最新的模型列表请使用 `llm models` 命令查看。

### 代理问题与解决方案

如果系统设置了 `socks://` 代理，`llm-ollama` 插件可能因依赖库不兼容而崩溃。

**临时方案**：运行 `llm` 命令前清除所有代理环境变量。

```bash
ALL_PROXY="" all_proxy="" HTTP_PROXY="" HTTPS_PROXY="" http_proxy="" https_proxy="" llm -m qwen-turbo "你好"
```

**持久化方案**：在 `~/.bashrc`（或 `~/.zshrc`）中添加别名。

```bash
alias llm='ALL_PROXY="" all_proxy="" HTTP_PROXY="" HTTPS_PROXY="" http_proxy="" https_proxy="" llm'
```

添加后执行 `source ~/.bashrc` 或重新打开终端即可生效。

## 基本使用

### 查看可用模型

```bash
llm models
```

### 执行提示词

```bash
# 使用默认模型
llm "你好"

# 指定模型
llm -m qwen-turbo "解释一下量子计算"

# 使用系统提示词
llm -m deepseek-v3.2 -s "你是一个编程老师" "解释递归"

# 管道输入
cat code.py | llm -m qwen3-coder-plus "审查这段代码"

# 启动多轮对话模式
llm chat -m qwen3.6-plus
```

### 常用参数

| 参数 | 说明 |
|------|------|
| `-m, --model` | 指定模型 |
| `-s, --system` | 系统提示词 |
| `-n, --no-log` | 不记录到数据库 |
| `-c, --continue` | 继续上次对话 |
| `-a, --attachment` | 附件（图片等） |
| `-o, --option` | 模型选项 |
| `-t, --template` | 使用模板 |

### 管理别名

```bash
# 设置别名
llm aliases set my-ai qwen3.6-plus

# 使用别名
llm -m my-ai "你好"
```

## 日志管理

`llm` 默认将所有对话记录到 SQLite 数据库，便于查询和管理。

```bash
# 查看最近的 5 条对话记录
llm logs -n 5

# 查看特定模型的对话记录
llm logs -m qwen-turbo

# 单次命令关闭日志记录
llm -m qwen-turbo "你好" --no-log
```

## 模型清单

> **提示**：以下是通过阿里云百炼可调用的部分模型示例，实际可用模型会动态更新，请以 `llm models` 命令的输出为准。

| 类别 | 模型 |
|------|------|
| 千问旗舰 | qwen3-max, qwen3.6-plus, qwen-max |
| 千问均衡 | qwen-plus, qwen3.5-plus |
| 千问快速 | qwen3.5-flash, qwen-flash, qwen-turbo |
| 代码 | qwen-coder-plus, qwen3-coder-plus, qwen3-coder-flash |
| 视觉 | qwen-vl-max, qwen3-vl-plus, qwen3-vl-flash |
| 推理 | qwq-plus, qwq-32b |
| 长文本 | qwen-long |
| 数学 | qwen-math-plus |
| 深度研究 | qwen-deep-research |
| 翻译 | qwen-mt-plus |
| DeepSeek | deepseek-v3.2, deepseek-v3.1, deepseek-v3, deepseek-r1 |
| GLM | glm-5, glm-4.7, glm-4.6, glm-4.5 |
| Kimi | kimi-k2.5, kimi-k2-thinking |
| MiniMax | minimax-m2.7, minimax-m2.5 |
| 零一万物 | yi-large, yi-large-turbo, yi-medium |
| 百川 | baichuan2-turbo |
| Llama | llama-4-maverick, llama3.3-70b, llama3.1-405b |

## 常见问题

### 1. `llm keys set` 输入无效

**现象**：运行 `llm keys set openai` 后，输入的 Key 没有被正确保存，`keys.json` 中的值变成了 `"Enter key: "`。

**原因**：某些终端环境可能导致回显控制失效（`GetPassWarning`），使得 `llm` 捕获了提示文本而非实际输入。

**解决**：直接手动编辑 `keys.json` 文件：

```bash
# 找到配置文件路径
python3 -c "from llm import user_dir; print(user_dir() / 'keys.json')"
# 文件通常位于 ~/.config/io.datasette.llm/keys.json

# 直接编辑文件，写入正确的 Key
```

`keys.json` 格式：

```json
{
  "// Note": "This file stores secret API credentials. Do not share!",
  "openai": "sk-你的真实API密钥"
}
```

### 2. 自定义模型未被识别

**现象**：配置了 `extra-openai-models.yaml` 后，`llm models` 仍然看不到自定义模型。

**原因**：`llm` 的 OpenAI 插件内置了模型白名单，不会自动从自定义端点拉取模型列表。

**解决**：确保配置文件格式正确。每个模型条目必须同时指定 `model_id`、`model_name`、`api_base` 和 `api_key_name` 四个字段：

```yaml
- model_id: qwen-turbo          # 在 llm 中使用的名称
  model_name: qwen-turbo        # 实际传递给 API 的名称
  api_base: "https://dashscope.aliyuncs.com/compatible-mode/v1"
  api_key_name: openai          # 对应 keys.json 中的键名，用于查找密钥
```

配置完成后运行 `llm models` 验证，新模型应出现在列表中。
