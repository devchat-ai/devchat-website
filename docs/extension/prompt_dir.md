---
id: prompt-dir
slug: /extend-devchat-with-custom-prompts
description: Extend chats with user-defined prompts
sidebar_position: 1
---

# Prompt Directory

The prompt directory is designed to support simple prompt template extension. It is a regular file directory that can be easily managed and edited. You don't need to learn a programming languague framework to do prompt engineering.

By default, the directory is named `workflows` and located in the `.chat` folder at your home directory. You can run `ls ~/.chat/workflows` in a terminal to see what's inside.

## Path

The `workflows` directory contains three subdirectories, `sys`, `org`, and `usr`. The `sys` (system) directory is a clone of https://github.com/devchat-ai/workflows, which contains the default prompt templates. You can overwrite those system prompts. For instance, if you create `commit_message` in the `usr` directory and define your own `prompt.txt`, DevChat will use your version instead of the default one in `sys`, for the command `commit_message`.

  ```
  workflows
  ├── sys
  │   └── commit_message
  │       └── prompt.txt
  ├── org
  │   └── commit_message
  │       └── prompt.txt
  └── usr
      └── commit_message
          └── prompt.txt
  ```

In addition to `sys` and `usr`, the `org` directory is reserved for team-wise conventions. For instance, if your team requires a docstring for every method, you may add this requirement to the default prompt for the `code` command. Consequently, DevChat will adhere to this requirement when generating code.

Your team can maintain a Git repository to store prompts for `org`, and every team member can locally sync `org` with the repository. The team-wise prompts will overwrite those in `sys`, while you can still further customize them for yourself by providing any in `usr`.

## Command Name

You can utilize a prompt template by typing a "command" with the corresponding name in the DevChat input. Type `/` followed by the command name.

  <img width="386" alt="image" src="https://github.com/devchat-ai/devchat-vscode/assets/592493/145d94eb-a3e8-42ca-bb88-a462b6070b2f" />

  The `/`-separated path to a directory corresponds to a `.`-separated command name. For instance, if your prompt is located in the directory `path/to/dir`, you would represent this as the command `/path.to.dir` in the DevChat input. Note that `sys`, `org`, or `usr` do not need to be included in a command name. DevChat will first look up the corresponding path under `usr`, then `org`, and finally `sys`.

## Inheritance

By default, a command will incorporate the `prompt.txt` file in the corresponding directory and all the `prompt.txt` files in the parent and ancestor directories. For example, if you want to write a general `code` template with specific requirements for different programming languages, the prompts can be organized as follows:

  ```
  workflows
  └── usr
      └── code
          ├── prompt.txt
          ├── go
          │   └── prompt.txt
          ├── js
          │   └── prompt.txt
          └── py
              └── prompt.txt
  ```

  When you type `/code.py` in DevChat, it will include both `prompt.txt` in `usr/code/` and `prompt.txt` in `usr/code/py/`. This structure aligns with our `sys` directory. You can refer to the contents of [sys/code/prompt.txt](https://github.com/devchat-ai/workflows/blob/main/code/prompt.txt) and [sys/code/py/prompt.txt](https://github.com/devchat-ai/workflows/blob/main/code/py/prompt.txt) for more details.
