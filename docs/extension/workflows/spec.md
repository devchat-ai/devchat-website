---
slug: /devchat-workflow-specification
description: Specification of workflows
sidebar_position: 3
---

# Workflow Specification

Chatting with AI can facilitate and drive specific workflows for developers.
These workflows range from straightforward tasks like composing a commit message to more complex processes with multiple steps like searching for relevant information and answering a code-related question.

In DevChat, a **workflow** consists of three components:
- Main Command: This command outlines the series of steps to perform in the workflow. Each step can involve either a chat with the AI or the execution of a script.
- Context: This is a designated file storing essential data or prompts for the main command. Every step within the main command may optionally access or modify the context.
- User Input: This captures and stores the information entered by the user, allowing the main command to reference it when needed.

Technically, a workflow is represented by the YAML file of the main command.
The steps of the command can reference the context and user input by using the `{context}` and `{input}` keywords, respectively.