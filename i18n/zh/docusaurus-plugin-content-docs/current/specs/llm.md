---
slug: /llm
title: 注解调用LLM
description: 通过Python注解方便的调用LLM。
sidebar_position: 6
---

# 注解调用 LLM

当你开发 Python 智能脚本时，你可以使用`@chat`注解来调用 LLM。

### 安装

```bash
pip install devchat
```

### 参数说明

@chat 注解函数支持 5 个参数，分别是：

- prompt：提示词模板，支持使用占位符，如示例中的 `{file_path}`、`{selected_text}` 等。
- memory：对话记忆，用于存储历史对话。
- stream_out：是否将输出流输出。
- model：LLM 模型名称，默认是 `gpt-3.5-turbo-1106`。
- llm_config：LLM 配置，如 temperature、top_p 等。

```python
def chat(
    prompt,
    memory: ChatMemory = None,
    stream_out: bool = False,
    model: str = os.environ.get("LLM_MODEL", "gpt-3.5-turbo-1106"),
    **llm_config,
)
```

### 调用示例

```python
# 导入注解函数——chat
from devchat.llm import chat

# 定义提示词、示例，以形成对话记忆
MESSAGES_FEW_SHOT = [
    {
        "role": "system",
        "content": """
您是一名代码助手。您的任务是为给定的代码块添加注释。
要添加注释，您需要遵循以下规则：
1. 请勿更改代码块中的任何代码，甚至包括空格字符；
........
"""
    },
]
memory = FixSizeChatMemory(max_size=20, messages=MESSAGES_FEW_SHOT)

# 定义提示词模板
PROMPT_TEMPLATE = """
文件：
{file_path}

代码：
{selected_text}

代码块中注释请使用中文描述。
"""

# 为函数添加注解，输入参数将作为提示词参数，返回值将是LLM的输出
@chat(prompt=PROMPT_TEMPLATE, stream_out=True, memory=memory)
def add_comments(selected_text, file_path):
    """Call AI to rewrite selected code"""
    pass

def main():

    # 为了理解容易，我们没有增加IDE Service的调用代码
    # 假设从IDE Service中获取到了文件路径和代码片段
    file_path = "logger.ts"
    selected_text = """
        this.logEventToServer({
            completion_id: response!.id,
            type: "select",
            lines: response!.code.split('\\n').length,
            length: response!.code.length
        });
    """

    # 调用函数，并接收LLM结果
    response = add_comments(selected_text=selected_text, file_path=file_path)

    # 处理LLM输出结果
    print(response)

```
