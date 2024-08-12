---
title: 可移植 IDE 服务
slug: /portable-ide-service
sidebar_position: 4
---

# 可移植 IDE 服务

Portable IDE Service 提供了一个统一的接口来与不同的 IDE 进行交互。通过使用这个服务，您可以编写能够在多个 IDE 环境中运行的工具和插件，而无需为每个 IDE 编写特定的代码。如获取语言设置、记录日志、获取文档符号等。

这个服务涵盖了从基本的 IDE 信息查询到复杂的代码操作等多种功能，使得开发跨 IDE 的工具变得更加简单和高效。

## 初始化

要使用 IDE Service，首先需要创建一个 `IDEService` 实例：

```python
from lib.ide_service.service import IDEService

client = IDEService()
```

## 使用示例

以下是一个使用 IDE Service 的简单示例：

```python
from lib.ide_service.service import IDEService

# 创建 IDE Service 实例
ide_service = IDEService()

# 获取 IDE 语言
language = ide_service.ide_language()
print(f"Current IDE language: {language}")

# 获取选中的代码范围
selected_code = ide_service.get_selected_range()
print(f"Selected code: {selected_code.text}")

# 获取文档符号
symbols = ide_service.get_document_symbols("/path/to/your/file.py")
for symbol in symbols:
    print(f"Symbol: {symbol.name}, Kind: {symbol.kind}")

# 应用差异
new_content = "def hello_world():\n    print('Hello, World!')"
success = ide_service.diff_apply("/path/to/your/file.py", new_content)
if success:
    print("Changes applied successfully")
else:
    print("Failed to apply changes")
```

## 函数列表

### ide_language()

获取当前 IDE 的语言设置。

```python
language = client.ide_language()
```

返回值：语言代码（"zh" 表示中文，"en" 表示英文）

### get_document_symbols(abspath: str)

获取指定文件的文档符号。

```python
symbols = client.get_document_symbols("/path/to/file.py")
```

参数：

- `abspath`: 文件的绝对路径

返回值：`SymbolNode` 对象列表

### find_type_def_locations(abspath: str, line: int, character: int)

查找类型定义的位置。

```python
locations = client.find_type_def_locations("/path/to/file.py", 10, 5)
```

参数：

- `abspath`: 文件的绝对路径
- `line`: 开始搜索的行号
- `character`: 开始搜索的字符位置

返回值：`Location` 对象列表

### find_def_locations(abspath: str, line: int, character: int)

查找定义的位置。

```python
locations = client.find_def_locations("/path/to/file.py", 10, 5)
```

参数：

- `abspath`: 文件的绝对路径
- `line`: 开始搜索的行号
- `character`: 开始搜索的字符位置

返回值：`Location` 对象列表

### ide_name()

获取 IDE 的名称。

```python
ide_name = client.ide_name()
```

返回值：IDE 名称（例如 "vscode" 或 "pycharm"）

### diff_apply(filepath, content, autoedit: bool = False)

应用差异到指定文件。

```python
success = client.diff_apply("/path/to/file.py", "new content", autoedit=True)
```

参数：

- `filepath`: 需要更新的文件路径
- `content`: 包含新代码的字符串
- `autoedit`: 是否自动编辑（默认为 False）

返回值：差异是否成功应用（布尔值）

### get_visible_range()

获取当前 IDE 中可见的代码范围。

```python
visible_range = client.get_visible_range()
```

返回值：`LocationWithText` 对象

### get_selected_range()

获取当前 IDE 中选中的代码范围。

```python
selected_range = client.get_selected_range()
```

返回值：`LocationWithText` 对象

### get_diagnostics_in_range(fileName: str, startLine: int, endLine: int)

获取指定范围内的诊断信息。

```python
diagnostics = client.get_diagnostics_in_range("/path/to/file.py", 1, 10)
```

参数：

- `fileName`: 文件名
- `startLine`: 起始行
- `endLine`: 结束行

返回值：诊断消息列表（字符串列表）

### get_collapsed_code(fileName: str, startLine: int, endLine: int)

获取指定范围外的折叠代码。

```python
collapsed_code = client.get_collapsed_code("/path/to/file.py", 1, 10)
```

参数：

- `fileName`: 文件名
- `startLine`: 起始行
- `endLine`: 结束行

返回值：折叠的代码（字符串）

### get_extension_tools_path()

获取扩展工具路径。

```python
tools_path = client.get_extension_tools_path()
```

返回值：扩展工具路径（字符串）

### select_range(fileName: str, startLine: int, startColumn: int, endLine: int, endColumn: int)

在指定文件中选择一个文本范围。

```python
success = client.select_range("/path/to/file.py", 1, 0, 5, 10)
```

参数：

- `fileName`: 文件名
- `startLine`: 选择起始行（从 0 开始）
- `startColumn`: 选择起始列（从 0 开始）
- `endLine`: 选择结束行（从 0 开始）
- `endColumn`: 选择结束列（从 0 开始）

返回值：选择是否成功（布尔值）

注意：如果 `startLine` 为 -1，则取消当前选择。
