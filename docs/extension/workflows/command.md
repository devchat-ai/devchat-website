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

For example, we can create a command `tree` to list directory files, as defined in the following YAML file:

```yaml
```

By convention, this file should be named `command.yml` and placed in the [prompt directory](/extend-devchat-with-custom-prompts).
Once set up, you can invoke the command in DevChat with `/tree`, if it resides in `.chat/workflows/usr/tree/command.yml` within your home directory.
The path and naming conventions for commands adhere to the [Prompt Directory specifications](/extend-devchat-with-custom-prompts#path).
