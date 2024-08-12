---
title: Portable IDE Service
slug: /portable-ide-service
sidebar_position: 4
---

# Portable IDE Service

The Portable IDE Service provides a unified interface for interacting with different IDEs. By using this service, you can write tools and plugins that run in multiple IDE environments without having to write specific code for each IDE. It allows you to perform tasks such as retrieving language settings, logging, and obtaining document symbols.

This service covers a wide range of functionalities, from basic IDE information queries to complex code operations, making it simpler and more efficient to develop cross-IDE tools.

## Initialization

To use the IDE Service, you first need to create an `IDEService` instance:

```python
from lib.ide_service.service import IDEService

client = IDEService()
```

## Usage Example

Here's a simple example of using the IDE Service:

```python
from lib.ide_service.service import IDEService

# Create an IDE Service instance
ide_service = IDEService()

# Get the IDE language
language = ide_service.ide_language()
print(f"Current IDE language: {language}")

# Get the selected code range
selected_code = ide_service.get_selected_range()
print(f"Selected code: {selected_code.text}")

# Get document symbols
symbols = ide_service.get_document_symbols("/path/to/your/file.py")
for symbol in symbols:
    print(f"Symbol: {symbol.name}, Kind: {symbol.kind}")

# Apply differences
new_content = "def hello_world():\n    print('Hello, World!')"
success = ide_service.diff_apply("/path/to/your/file.py", new_content)
if success:
    print("Changes applied successfully")
else:
    print("Failed to apply changes")
```

## Function List

### ide_language()

Get the current IDE's language setting.

```python
language = client.ide_language()
```

Return value: Language code ("zh" for Chinese, "en" for English)

### get_document_symbols(abspath: str)

Get document symbols for the specified file.

```python
symbols = client.get_document_symbols("/path/to/file.py")
```

Parameters:

- `abspath`: Absolute path of the file

Return value: List of `SymbolNode` objects

### find_type_def_locations(abspath: str, line: int, character: int)

Find type definition locations.

```python
locations = client.find_type_def_locations("/path/to/file.py", 10, 5)
```

Parameters:

- `abspath`: Absolute path of the file
- `line`: Line number to start searching
- `character`: Character position to start searching

Return value: List of `Location` objects

### find_def_locations(abspath: str, line: int, character: int)

Find definition locations.

```python
locations = client.find_def_locations("/path/to/file.py", 10, 5)
```

Parameters:

- `abspath`: Absolute path of the file
- `line`: Line number to start searching
- `character`: Character position to start searching

Return value: List of `Location` objects

### ide_name()

Get the name of the IDE.

```python
ide_name = client.ide_name()
```

Return value: IDE name (e.g., "vscode" or "pycharm")

### diff_apply(filepath, content, autoedit: bool = False)

Apply differences to the specified file.

```python
success = client.diff_apply("/path/to/file.py", "new content", autoedit=True)
```

Parameters:

- `filepath`: Path of the file to update
- `content`: String containing the new code
- `autoedit`: Whether to auto-edit (default is False)

Return value: Boolean indicating whether the differences were successfully applied

### get_visible_range()

Get the visible code range in the current IDE.

```python
visible_range = client.get_visible_range()
```

Return value: `LocationWithText` object

### get_selected_range()

Get the selected code range in the current IDE.

```python
selected_range = client.get_selected_range()
```

Return value: `LocationWithText` object

### get_diagnostics_in_range(fileName: str, startLine: int, endLine: int)

Get diagnostic information within the specified range.

```python
diagnostics = client.get_diagnostics_in_range("/path/to/file.py", 1, 10)
```

Parameters:

- `fileName`: File name
- `startLine`: Start line
- `endLine`: End line

Return value: List of diagnostic messages (list of strings)

### get_collapsed_code(fileName: str, startLine: int, endLine: int)

Get collapsed code outside the specified range.

```python
collapsed_code = client.get_collapsed_code("/path/to/file.py", 1, 10)
```

Parameters:

- `fileName`: File name
- `startLine`: Start line
- `endLine`: End line

Return value: Collapsed code (string)

### get_extension_tools_path()

Get the extension tools path.

```python
tools_path = client.get_extension_tools_path()
```

Return value: Extension tools path (string)

### select_range(fileName: str, startLine: int, startColumn: int, endLine: int, endColumn: int)

Select a text range in the specified file.

```python
success = client.select_range("/path/to/file.py", 1, 0, 5, 10)
```

Parameters:

- `fileName`: File name
- `startLine`: Selection start line (0-based)
- `startColumn`: Selection start column (0-based)
- `endLine`: Selection end line (0-based)
- `endColumn`: Selection end column (0-based)

Return value: Boolean indicating whether the selection was successful

Note: If `startLine` is -1, the current selection is cleared.
