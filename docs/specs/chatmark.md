---
id: chatmark
slug: /chatmark-markdown-spec
description: the DevChat Flavored Markdown
sidebar_position: 5
---

# ChatMark: the DevChat Flavored Markdown

ChatMark enhances standard markdown by introducing GUI elements within code blocks. Within a ChatMark block, you'll find normal text alongside specialized widgets, denoted by paragraphs starting with `>` (namely, quoted). Between different widgets, there must be at least a blank line or a line of normal text. The reply to a widget is typically in the form of single values or multiple key-value pairs, all adhering to YAML syntax.

## Widgets

### Checkbox

The checkbox widget in ChatMark is structured as follows, residing inside a ChatMark block.

`> [status](ID) Title`

- The status `[ ]` or `[x]` indicates if the checkbox is unchecked or checked, respectively.
- The ID in parentheses is a unique identifier for referencing the item.
- The text following the ID describes the checkbox item.
- The reply should be ID-status pairs.

Example:

````
```chatmark
Which files would you like to commit? I've suggested a few.
> [x](file1) devchat/engine/prompter.py
> [x](file2) devchat/prompt.py
> [](file3) tests/test_cli_prompt.py
```
````

An example reply in YAML:

````
```yaml
file1: checked
file3: checked
```
````

### Radio Button

The radio button widget in ChatMark is structured as follows, residing inside a ChatMark block.

`> - (ID) Title`

- The ID in parentheses is a unique identifier for referencing the item.
- The text following the ID describes the item.
- The reply should be a single ID referencing the selected item.

Example:

````
```chatmark
How would you like to make the change?
> - (insert) Insert the new code.
> - (new) Put the code in a new file.
> - (replace) Replace the current code.
```
````

An example reply in YAML:

````
```yaml
replace: checked
```
````

### Editor

Inside a ChatMark block, quoted text without any other widget format is rendered to an editable text input.

Example:

````
```chatmark
I've drafted a commit message for you as below. Feel free to modify it.

> | (ID)
> fix: prevent racing of requests
>
> Introduce a request id and a reference to latest request. Dismiss
> incoming responses other than from latest request.
>
> Reviewed-by: Z
> Refs: #123
```
````

The reply should contain the full text in the quoted format with or without any modification.

````
```yaml
ID: |
    fix: prevent racing of requests
    
    Introduce a request ID and a reference to latest request. Dismiss
    incoming responses other than from latest request.
    
    Reviewed-by: Z
    Refs: #123
```
````

Note that, in a reply, the YAML block scalar (`|`) is primarily used for multi-line strings where line breaks need to be preserved. It is not necessary for single-line texts. For example, `ID: "fix: prevent racing of requests"` is a valid reply. Quotation marks can be used around single-line strings but are not mandatory unless the string contains special characters that might be misinterpreted, such as a colon.

## Forms

## Buttons

The button widget in ChatMark is structured as follows, residing inside a ChatMark block.

`> (ID) Title`
- The ID in parentheses is a unique identifier for referencing the button.
- The text following the ID shows on the button.
- The reply should be a single ID referencing the clicked button.

Example:

````
```chatmark
Would you like to pay $0.02 for this LLM query?
> (Confirm) Yes, go ahead!
> (Cancel) No, let's skip this.
```
````
