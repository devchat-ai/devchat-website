---
id: inter-commmand-communication
slug: /devchat-inter-commmand-communication
description: Inter-command communication in DevChat
sidebar_position: 2
---

# Inter-Command Communication

Commands in DevChat can communicate with each other through temporary files and pipes.

Two default temporary files are available for every command in a workflow environment: `{context}` and `{input}`.
Those keywords are replaced with the actual file paths when the command is executed.

Pipes are used in two main scenarios:
1. User interaction: By default, a command's standard input is configured to accept continuous input from the user, while its standard output streams data back to the user.
2. Command chaining: Pipes allow the output of one command to feed directly into the input of another.

## Temporary Files

To facilitate access by multiple commands and enhance content presentation within the UI, we've established a fundamental structure for the context file.
This ensures simplicity while retaining flexibility for user-defined commands.

The context file is a collection of sections enclosed by `<context>` tags.
The `<context>` element acts as a container for any content that a command may need to store.
Additionally, attributes like location and type of the original content can be appended to this tag.

For location specification, DevChat adheres to a convention where the `uri` attribute denotes the path (e.g., `file:///C:/Users/User/project/code.py`), and the `range` attribute, expressed as a JSON object, indicates the specific lines and characters. An example is given below.

```json
{
    start: { line: 5, character: 23 },
    end : { line: 6, character: 0 }
}
```

Our approach aligns with the [Language Server Protocol](https://microsoft.github.io/language-server-protocol/)'s standards for [URI formatting](https://microsoft.github.io/language-server-protocol/specifications/specification-current/#uri) and [range structuring](https://microsoft.github.io/language-server-protocol/specifications/specification-current/#range).

## Pipes