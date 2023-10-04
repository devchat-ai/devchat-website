---
id: inter-commmand-communication
slug: /devchat-inter-commmand-communication
description: Inter-command communication in DevChat
sidebar_position: 2
---

# Inter-Command Communication

Commands in DevChat can communicate with each other through pipes.
Typically, we use two forms of pipes.
The first form is to chain commands by redirecting the standard output of one command to the standard input of another command.

The second form is to use named pipes over the `{context}` and `{input}` files.