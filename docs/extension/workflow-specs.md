---
id: workflow-specs
sidebar_position: 2
description: Extend chats with user-defined operations
---

# Workflow Specifications

## Command

The **command** is a consolidated representation of an operation in a chat with AI.
Such an operation can either provide information to the chat or be triggered by AI to perform tasks beyond mere texting.
The *unified* command definition applies to LLM calls, scripts, and other user interfaces.
Consequently, users only need to define a command once in an easy-to-ready YAML file, enabling its use as LLM functions, script execution, and UI integration.

For example, we can create a command `tree` to list directory files.

## Workflow

Interacting with AI involves more than just messaging. Within software development, it facilitates and drives specific workflows. These workflows can range from straightforward tasks like composing a commit message to more complex processes with multiple steps like searching for relevant information and answering a code-related question.

In DevChat, a **workflow** is structured around three components:
- Main Command: This outlines the series of steps needed. Each step can involve either a chat with the AI or the execution of a script.
- Context: This is a designated file storing essential data or prompts for the main command. Every step within the main command may optionally access or modify the context.
- User Input: This captures and stores the information entered by the user, allowing the main command to reference it when needed.
