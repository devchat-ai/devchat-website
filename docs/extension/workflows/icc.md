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

To facilitate access by multiple commands and enhance content presentation within the UI, we've established a basic structure for the context file.
This ensures simplicity while retaining flexibility for user-defined commands.

The context file is a collection of sections enclosed by `<context>` tags.
The `<context>` element acts as a container for any content that a command may need to store and provide to AI.
Additionally, attributes like location and type of the original content of a context can be appended to this tag.

For location specification, DevChat recommends a convention where the `uri` attribute denotes the path (e.g., `uri="file:///C:/Users/User/project/code.py"`), and the `range` attribute, expressed as a JSON object, indicates the specific lines and characters (e.g., `range="{start: {line: 5, character: 23}, end: {line: 6, character: 0}}"`).

Our approach aligns with the [Language Server Protocol](https://microsoft.github.io/language-server-protocol/) (LSP)'s standards for [URI formatting](https://microsoft.github.io/language-server-protocol/specifications/specification-current/#uri) and [range structuring](https://microsoft.github.io/language-server-protocol/specifications/specification-current/#range).
Note that the `uri` format, designed primarily for enhanced human readability, is not strict.
Alternatively, you may use the `path` attribute to specify an absolute or relative path.
Remember, these attributes are optional and can be left out when irrelevant.

There's also a `language` attribute available to specify the programming language of the content.
When setting this attribute, it's advisable to ensure the value conforms to the [LSP's language identifiers](https://microsoft.github.io/language-server-protocol/specifications/specification-current/#textDocumentItem).

## Pipes

For user interaction, 