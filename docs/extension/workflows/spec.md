---
slug: /devchat-workflow-specification
description: Specification of workflows
sidebar_position: 3
---

# Workflow Specification

Chatting with AI can facilitate and drive specific workflows for developers.
These workflows range from straightforward tasks, such as composing a commit message, to more complex processes with multiple steps, such as searching for relevant information and answering a code-related question.

In DevChat, a **workflow** consists of three components:
- Command: This outlines the steps to perform the workflow. Each step can involve either a chat with the AI or the execution of a script.
- Context: This stores essential data or prompts for the workflow. Every step within the command may optionally access or modify the context.
- User Input: This captures and stores the information entered by the user, allowing the command to reference it when needed.

Technically, a workflow is represented by the YAML file of the command, and any step of the command can reference the context and user input files by using the `{context}` and `{input}` keywords, respectively.