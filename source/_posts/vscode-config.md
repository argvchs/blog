---
title: VSCode 配置教程
date: 2023-08-28 14:54:05
tags:
    - VSCode
categories: 教程
---

面向 OIer 的 VSCode 配置教程。

<!-- more -->

# 1. 安装 Motrix

<https://motrix.app>

安装后就可以用 Motrix 快速下载了。

# 2. 安装 VSCode

<https://code.visualstudio.com>

Windows 7: <https://code.visualstudio.com/updates/v1_70>

# 3. 安装编译器

<https://winlibs.com>

选择 Release versions 里面的最新版本下载。

解压到合适的位置然后将其中的 `mingw64/bin` 添加到环境变量。

# 4. 安装字体

-   Fira Code

    <https://github.com/tonsky/FiraCode/releases>

    解压后安装 `ttf` 下的所有字体。

-   Source Han Sans

    <https://github.com/adobe-fonts/source-han-sans/releases>

    下载 Region Specific Subset OTFs Simplified Chinese 这个版本。

    解压后安装 `SubsetOTF/CN` 下的所有字体。

若 GitHub 打不开可以将 `github.com` 替换为 `githubfast.com`。

# 5. 安装 Git Bash

<https://git-scm.com/download/win>

安装 Git Bash 是因为 Windows CMD 太难用了。

# 6. 安装扩展

打开 VSCode 然后安装以下扩展：

1. C++ Extension Pack
2. Code Runner
3. Competitive Programming Helper (cph)
4. One Dark Pro
5. vscode-icons
6. Fluent Icons
7. Markdown Preview Github Styling
8. Prettier
9. Chinese (Simplified) Language Pack for Visual Studio Code

有些教程说要配置 `launch.json` `tasks.json` 才能运行，但是这样太麻烦了。

我们安装 Code Runner 扩展后按 `Ctrl+Alt+N` 就可以了，或者你可以直接用 CPH。

# 7. 创建文件夹

在一个合适的位置创建一个合适的文件夹用于存储你所有的 C++ 文件。

然后在里面创建 `.vscode` 文件夹用于存储配置文件，有两个配置文件，创建完成后目录结构应为如下：

```
|---.vscode
    |---settings.json
    |---c_cpp_properties.json
```

# 8. 配置 `settings.json`

这个 `settings.json` 是我的配置。

```json
{
    "[json]": { "editor.defaultFormatter": "esbenp.prettier-vscode" },
    "[jsonc]": { "editor.defaultFormatter": "esbenp.prettier-vscode" },
    "C_Cpp.autoAddFileAssociations": false,
    "C_Cpp.clang_format_fallbackStyle": "{ BasedOnStyle: LLVM, AccessModifierOffset: -2, AlwaysBreakTemplateDeclarations: true, AllowShortBlocksOnASingleLine: true, AllowShortCaseLabelsOnASingleLine: true, AllowShortEnumsOnASingleLine: true, AllowShortFunctionsOnASingleLine: true, AllowShortIfStatementsOnASingleLine: AllIfsAndElse, AllowShortLambdasOnASingleLine: All, AllowShortLoopsOnASingleLine: true, ColumnLimit: 100, FixNamespaceComments: false, IndentWidth: 4, TabWidth: 4, UseTab: Never }",
    "code-runner.executorMap": {
        "c": "gcc $fileName -o $fileNameWithoutExt -std=c17 -Wall -O2 && ./$fileNameWithoutExt",
        "cpp": "g++ $fileName -o $fileNameWithoutExt -std=c++20 -Wall -O2 && ./$fileNameWithoutExt"
    },
    "code-runner.fileDirectoryAsCwd": true,
    "code-runner.ignoreSelection": true,
    "code-runner.runInTerminal": true,
    "cph.language.c.Args": "-std=c17 -Wall -O2",
    "cph.language.c.Command": "gcc",
    "cph.language.cpp.Args": "-std=c++20 -Wall -O2",
    "cph.language.cpp.Command": "g++",
    "debug.console.fontFamily": "'Fira Code', 'Source Han Sans SC'",
    "editor.bracketPairColorization.enabled": false,
    "editor.codeLensFontFamily": "'Fira Code', 'Source Han Sans SC'",
    "editor.cursorBlinking": "phase",
    "editor.cursorSmoothCaretAnimation": "on",
    "editor.cursorStyle": "block",
    "editor.fontFamily": "'Fira Code', 'Source Han Sans SC'",
    "editor.fontLigatures": true,
    "editor.fontWeight": "500",
    "editor.minimap.maxColumn": 30,
    "editor.minimap.renderCharacters": false,
    "editor.minimap.scale": 3,
    "editor.renderWhitespace": "boundary",
    "editor.wordWrap": "on",
    "explorer.confirmDelete": false,
    "explorer.confirmDragAndDrop": false,
    "explorer.sortOrder": "type",
    "files.associations": {
        "*.in": "plaintext",
        "*.out": "plaintext",
        "*.ans": "plaintext"
    },
    "files.autoGuessEncoding": true,
    "markdown.preview.fontFamily": "'Fira Code', 'Source Han Sans SC'",
    "prettier.printWidth": 100,
    "prettier.tabWidth": 4,
    "search.followSymlinks": false,
    "terminal.integrated.defaultProfile.windows": "Git Bash",
    "terminal.integrated.enableMultiLinePasteWarning": false,
    "terminal.integrated.fontFamily": "'Fira Code', 'Source Han Sans SC'",
    "terminal.integrated.letterSpacing": 1,
    "terminal.integrated.rightClickBehavior": "default",
    "window.menuBarVisibility": "compact",
    "window.zoomLevel": 0,
    "workbench.colorTheme": "One Dark Pro Mix",
    "workbench.editor.pinnedTabSizing": "compact",
    "workbench.iconTheme": "vscode-icons",
    "workbench.productIconTheme": "fluent-icons",
    "workbench.tree.indent": 20
}
```

# 9. 配置 `c_cpp_properties.json`

注意下面的 `path/to/mingw64/bin/gcc.exe` 要换成你的编译器路径。

```json
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": ["${workspaceFolder}/**"],
            "defines": ["_DEBUG", "UNICODE", "_UNICODE"],
            "compilerPath": "path/to/mingw64/bin/gcc.exe",
            "cStandard": "c17",
            "cppStandard": "c++20",
            "intelliSenseMode": "windows-gcc-x64"
        }
    ],
    "version": 4
}
```

# VSCode，启动！
