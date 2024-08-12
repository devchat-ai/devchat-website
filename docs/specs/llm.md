---
slug: /llm
title: Annotation to Call LLM
description: Easily call LLM through Python annotations.
sidebar_position: 6
---

# Annotation to Call LLM

When you develop Python intelligent scripts, you can use the `@chat` annotation to call LLM.

### Installation

```bash
pip install devchat
```

### Parameter Description

The @chat annotation function supports 5 parameters, which are:

- prompt: The prompt template, which supports the use of placeholders, such as `{file_path}` and `{selected_text}` in the example.
- memory: The conversation memory, used to store historical conversations.
- stream_out: Whether to output the stream.
- model: The name of the LLM model, the default is `gpt-3.5-turbo-1106`.
- llm_config: The LLM configuration, such as temperature, top_p, etc.

```python
def chat(
    prompt,
    memory: ChatMemory = None,
    stream_out: bool = False,
    model: str = os.environ.get("LLM_MODEL", "gpt-3.5-turbo-1106"),
    **llm_config,
)
```

### Call Example

```python
# Import the annotation function - chat
from devchat.llm import chat

# Define the prompt and examples to form the conversation memory
MESSAGES_FEW_SHOT = [
    {
        "role": "system",
        "content": """
You are a code assistant. Your task is to add comments to the given code block.
To add comments, you need to follow these rules:
1. Do not change any code in the code block, even including space characters;
........
"""
    },
]
memory = FixSizeChatMemory(max_size=20, messages=MESSAGES_FEW_SHOT)

# Define the prompt template
PROMPT_TEMPLATE = """
File:
{file_path}

Code:
{selected_text}

Please use Chinese to describe the comments in the code block.
"""

# Add an annotation to the function. The input parameters will be used as the prompt parameters, and the return value will be the output of the LLM
@chat(prompt=PROMPT_TEMPLATE, stream_out=True, memory=memory)
def add_comments(selected_text, file_path):
    """Call AI to rewrite selected code"""
    pass

def main():

    # For ease of understanding, we have not added the code to call the IDE Service
    # Assume that the file path and code snippet are obtained from the IDE Service
    file_path = "logger.ts"
    selected_text = """
        this.logEventToServer({
            completion_id: response!.id,
            type: "select",
            lines: response!.code.split('\\n').length,
            length: response!.code.length
        });
    """

    # Call the function and receive the LLM result
    response = add_comments(selected_text=selected_text, file_path=file_path)

    # Process the LLM output result
    print(response)
```
