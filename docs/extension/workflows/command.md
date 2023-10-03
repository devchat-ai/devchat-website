---
slug: /devchat-command-definition
description: Unified definition of operations in chatting
sidebar_position: 1
---

# Command

The **command** is a consolidated representation of an operation in a chat with AI.
Such an operation can either provide information to the chat or be triggered by AI to perform tasks beyond mere texting.
The *unified* command definition applies to LLM calls, scripts, and other user interfaces.
Consequently, users only need to define a command once in an easy-to-ready YAML file, enabling its use as LLM functions, script execution, and UI integration.

For example, we can create a command `tree` to list directory files.
