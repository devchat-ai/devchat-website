---
slug: /devchat-command-definition
description: Unified definition of operations in a workflow
sidebar_position: 1
---

# Command

Interacting with AI involves more than just messaging.
The **command** is a consolidated representation of an operation in a chat with AI.
Such an operation can be triggered by the user to provide information to the chat, such as adding some code to the chat context; it can also be triggered by AI to perform certain tasks, such as making new directories and files.

The *unified* command definition applies to LLM calls, scripts, and other user interfaces.
Consequently, users only need to define a command once in an easy-to-read YAML file, enabling its use as LLM functions, script execution, and UI integration.

In the example below, we illustrate how to define a `tree`` command to list directory files, using a YAML file, and the multiple ways it can be used in DevChat.

```yaml
description: list contents of directories in a tree-like format
parameters:
  paths:
    description: Target directories to list.
    type: string
  level:
    description: Max display depth of the directory tree.
    type: integer
    default: 3
  ignore:
    description: Do not list those files that match the wild-card pattern.
    type: string
    default: "*.pyc"
```

By convention, this file should be named `command.yml` and placed in the [prompt directory](/extend-devchat-with-custom-prompts).
Assuming it is located in `~/.chat/workflows/usr/tree/`, a user can easily invoke the command with the DevChat UI by entering or choosing `/tree`.
Besides UI, the command can also be used to construct a workflow in DevChat.
For instance, one workflow step may go as `/tree --paths="." --level=3`.
Additionally, DevChat boasts a feature that translates the YAML file into the [GPT function](https://openai.com/blog/function-calling-and-other-api-updates) format, which can then be interpreted and executed by a LLM as needed.

The conventions for command paths and names adhere to the [Prompt Directory specifications](/extend-devchat-with-custom-prompts#path).
Unlike prompts, there is no inheritance among commands.
If a command relies on another, simply invoke the latter in a step of the former.
