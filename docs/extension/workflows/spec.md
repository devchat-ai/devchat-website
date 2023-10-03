---
slug: /devchat-workflow-specification
description: Specification of workflows
sidebar_position: 2
---

# Specification

Interacting with AI involves more than just messaging. Within software development, it facilitates and drives specific workflows. These workflows can range from straightforward tasks like composing a commit message to more complex processes with multiple steps like searching for relevant information and answering a code-related question.

In DevChat, a **workflow** is structured around three components:
- Main Command: This outlines the series of steps needed. Each step can involve either a chat with the AI or the execution of a script.
- Context: This is a designated file storing essential data or prompts for the main command. Every step within the main command may optionally access or modify the context.
- User Input: This captures and stores the information entered by the user, allowing the main command to reference it when needed.
