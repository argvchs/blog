---
title: VSCode 配置教程
date: 2023-08-28 14:54:05
tags:
    - VSCode
categories: 教程
---

面向 OIer 的 VSCode 配置教程。

<!-- more -->

# 1. 安装环境

## 1.0. 安装 Motrix（可选）

<https://motrix.app>

安装后就可以用 Motrix 快速下载了。

## 1.1. 安装 VSCode

Windows 10/11：<https://code.visualstudio.com>

Windows 7：<https://code.visualstudio.com/updates/v1_70>

## 1.2. 安装编译器

<https://winlibs.com>

选择 Release versions 里面的最新版本下载。

解压到合适的位置然后将其中的 `mingw64/bin` 添加到环境变量。

## 1.3. 安装 Git Bash

<https://git-scm.com/download/win>

安装 Git Bash 是因为 Windows CMD 太难用了。

## 1.4. 安装字体

-   Fira Code

    <https://github.com/tonsky/FiraCode/releases>

    解压后安装 `ttf` 下的所有字体即可。

-   Noto Sans CJK

    <https://github.com/notofonts/noto-cjk/blob/main/Sans/README.md>

    Windows 10/11：下载 Super OTC 这个字体。

    Windows 7：下载 Language-specific OTFs 中 Simplified Chinese 这个字体。

    解压后直接安装即可。

若 GitHub 打不开可以将 `github.com` 替换为 `githubfast.com`。

# 2. VSCode

## 2.1. 安装扩展

打开 VSCode 然后安装以下扩展：

1. C++ Extension Pack
2. Code Runner
3. Competitive Programming Helper (cph)
4. One Dark Pro
5. vscode-icons
6. Fluent Icons
7. Error Lens
8. Better Comments
9. Prettier
10. Github Markdown Preview
11. vscode-pdf
12. Chinese (Simplified) Language Pack for Visual Studio Code

有些教程说要配置 `launch.json` `tasks.json` 才能运行，但是这样太麻烦了。

我们安装 Code Runner 扩展后按 `Ctrl + Alt + N` 就可以了，或者你可以直接用 cph。

## 2.2. 创建文件夹

在一个合适的位置创建一个合适的文件夹用于存储你所有的 C++ 文件。

然后在里面创建 `.vscode` 文件夹用于存储配置文件，创建完成后目录结构应为如下：

```
cpp
|---.vscode
|   |---settings.json
|   |---c_cpp_properties.json
|---.clang-format
```

## 2.3. 配置文件

配置文件的内容：

```json
// settings.json
{
    "[json]": { "editor.defaultFormatter": "esbenp.prettier-vscode" },
    "[jsonc]": { "editor.defaultFormatter": "esbenp.prettier-vscode" },
    "[yaml]": { "editor.tabSize": 4 },
    "C_Cpp.autoAddFileAssociations": false,
    "code-runner.executorMap": {
        "c": "gcc $fileName -o $fileNameWithoutExt -std=c17 -Wall -O2 && ./$fileNameWithoutExt",
        "cpp": "g++ $fileName -o $fileNameWithoutExt -std=c++20 -Wall -O2 && ./$fileNameWithoutExt"
    },
    "code-runner.fileDirectoryAsCwd": true,
    "code-runner.ignoreSelection": true,
    "code-runner.runInTerminal": true,
    "cph.general.autoShowJudge": false,
    "cph.general.timeOut": 10000,
    "cph.language.c.Args": "-std=c17 -Wall -O2",
    "cph.language.c.Command": "gcc",
    "cph.language.cpp.Args": "-std=c++20 -Wall -O2",
    "cph.language.cpp.Command": "g++",
    "editor.bracketPairColorization.enabled": false,
    "editor.cursorBlinking": "phase",
    "editor.cursorSmoothCaretAnimation": "on",
    "editor.cursorStyle": "block",
    "editor.fontFamily": "'Fira Code', 'Noto Sans CJK SC'",
    "editor.fontLigatures": true,
    "editor.fontWeight": "500",
    "editor.minimap.maxColumn": 30,
    "editor.minimap.renderCharacters": false,
    "editor.minimap.scale": 3,
    "editor.renderWhitespace": "boundary",
    "editor.wordWrap": "on",
    "explorer.autoReveal": false,
    "explorer.confirmDelete": false,
    "explorer.confirmDragAndDrop": false,
    "explorer.sortOrder": "type",
    "files.associations": {
        "*.ans": "plaintext",
        "*.in": "plaintext",
        "*.out": "plaintext",
        ".clang-format": "yaml"
    },
    "files.autoGuessEncoding": true,
    "prettier.printWidth": 90,
    "prettier.tabWidth": 4,
    "search.followSymlinks": false,
    "terminal.integrated.defaultProfile.windows": "Git Bash",
    "terminal.integrated.enableMultiLinePasteWarning": false,
    "terminal.integrated.fontFamily": "'Fira Code', 'Noto Sans CJK SC'",
    "terminal.integrated.letterSpacing": 1,
    "workbench.colorTheme": "One Dark Pro Mix",
    "workbench.editor.pinnedTabSizing": "compact",
    "workbench.iconTheme": "vscode-icons",
    "workbench.productIconTheme": "fluent-icons",
    "workbench.tree.indent": 20
}

```

```json
// c_cpp_properties.json
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": ["${workspaceFolder}/**"],
            "compilerPath": "path/to/gcc.exe",
            "cStandard": "c17",
            "cppStandard": "c++20",
            "intelliSenseMode": "windows-gcc-x64"
        }
    ],
    "version": 4
}
```

```yaml
# .clang-format
BasedOnStyle: LLVM
AccessModifierOffset: -2
AlwaysBreakTemplateDeclarations: true
AllowShortBlocksOnASingleLine: Empty
AllowShortCaseLabelsOnASingleLine: true
AllowShortEnumsOnASingleLine: true
AllowShortFunctionsOnASingleLine: All
AllowShortIfStatementsOnASingleLine: AllIfsAndElse
AllowShortLambdasOnASingleLine: All
AllowShortLoopsOnASingleLine: true
ColumnLimit: 90
FixNamespaceComments: false
IndentWidth: 4
PenaltyExcessCharacter: 10
PenaltyIndentedWhitespace: 10
TabWidth: 4
UseTab: Never
```

这个配置的编译器用的是 GCC，如果你想用 Clang 可以自行修改。

如果是 Windows 7 要把 `editor.cursorSmoothCaretAnimation` 值改为 `true`。

还有上面的 `path/to/gcc.exe` 要换成你的编译器路径。

# 3. Clangd（可选）

Clangd 提供了比 IntelliSense 更好的语言服务器。

其实并不建议使用 Clangd，因为其处理大结构体数组时很慢，例如这样就可以卡崩 Clangd：

```cpp
struct node {
    int a, b;
} a[100000005];
```

但是有时 IntelliSense 因为玄学原因用不了，就只能用 Clangd 了。

## 3.1. 安装扩展

安装 clangd 扩展即可。

## 3.2. 配置文件

配置 Clangd 后的目录结构应为如下：

```
cpp
|---.vscode
|   |---settings.json
|---.clang-format
|---.clangd
```

没有 `c_cpp_properties.json` 是因为配置了 Clangd 就不需要 IntelliSense 的配置文件了。

需要添加或更改的配置文件内容：

```json
// settings.json
{
    "C_Cpp.intelliSenseEngine": "disabled",
    "editor.semanticTokenColorCustomizations": {
        "enabled": true,
        "rules": { "operator": "#c678dd", "operator.userDefined": { "bold": true } }
    },
    "files.associations": {
        "*.ans": "plaintext",
        "*.in": "plaintext",
        "*.out": "plaintext",
        ".clang-format": "yaml",
        ".clangd": "yaml"
    }
}
```

```yaml
# .clangd
CompileFlags:
    Add: [-std=c++20, -Wall]
    Compiler: clang++
Index:
    Background: Skip
InlayHints:
    Enabled: false
```

注意 `CompileFlags.Compiler` 必须为 `clang++`，因为 Clangd 语言服务器是基于 Clang 的，但是你编译的时候还是可以用 GCC。

# VSCode，启动！
