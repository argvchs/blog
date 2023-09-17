---
title: Common Luogu-Paste Script
date: 2023-09-17 22:01:53
tags:
    - 洛谷
categories: 其他
---

Common Luogu-Paste Script（简称 Common LS、CLS）是一个洛谷剪贴板模块规范。

<!-- more -->

# 1. 使用

## 1.1. 内容范围注释

使用内容范围注释 `// begin(end) module` 标记模块代码的内容，若没有则全文都为模块的内容。

这样做的原因是可以将模块代码填写在 Markdown 里代码高亮。

````markdown
```js
// begin module
console.log("Hello, World!");
// end module
```
````

**注释的格式必须和示例完全相同，否则可能无法识别。**

之后的示例中会省略掉内容范围注释。

## 1.2. `require`

导入一个剪贴板模块，注意要在前面添加 `await` 因为返回的是一个 `promise`。

```js
const mod = await require("00000001");
```

## 1.3. `module.exports`

导出模块。

```js
// paste: 00000001
module.exports = x => x * x;

// paste: 00000002
const square = await require("00000001");
console.log(square(10));
// output: 100
```

## 1.4. `exports`

导出模块，但是和 `module.exports` 用法不同。

```js
// paste: 00000001
exports.square = x => x * x;

// paste: 00000002
const mod = await require("00000001");
console.log(mod.square(10));
// output: 100
```

## 1.5. `encode` `decode`

为了使模块不那么显而易见我们添加了 `encode` `decode` 功能。

支持的格式有 `plain`、`base64`、`hex`，其中 `plain` 表示不编码。

```js
let text = 'console.log("Hello, World!")';
let code = encode.hex(text);
console.log(code);
// output: 63 6f 6e 73 6f 6c 65 2e 6c 6f 67 28 22 48 65 6c 6c 6f 2c 20 57 6f 72 6c 64 21 22 29
console.log(decode.hex(code));
// output: console.log("Hello, World!")
```

## 1.6. 编码注释

编码注释 `// encode <type>` 表示这个模块的内容的编码格式，若没有则为 `plain`。

```js
// paste: 00000001
// encode hex
63 6f 6e 73 6f 6c 65 2e 6c 6f 67 28 22 48 65 6c 6c 6f 2c 20 57 6f 72 6c 64 21 22 29

// paste: 00000002
requires("00000001");
// output: Hello World!
```

## 1.7. 自定义编码

你也可以自定义编码。

```js
encode.reverse = text => text.split("").reverse().join("");
decode.reverse = code => code.split("").reverse().join("");
```

# 2. 导入

## 2.1. Polyfill

将 CLS Polyfill 放到顶层模块代码的前面就可以了。

```js
const encode = {};
const decode = {};
const require = async path => {
    let response = await fetch("/paste/" + path + "?_contentOnly");
    let json = await response.json();
    let data = json.currentData.paste.data;
    let regexp1 = /^\/\/ begin module$((.|\n)*)^\/\/ end module$/gm;
    let regexp2 = /^\/\/ encode (\w+)$/gm;
    let source = regexp1.exec(data)?.[1] || data;
    let encode = regexp2.exec(data)?.[1] || "plain";
    source = decode[encode](source);
    source = `(async () => {
        let module = { exports: {} };
        await (async (exports, module) => {
            ${source};
        })(module.exports, module);
        return module.exports;
    })();`;
    return await eval(source);
};
encode.plain = text => text;
decode.plain = code => code;
encode.base64 = text => btoa(text);
decode.base64 = code => atob(code);
encode.hex = text => {
    let array = [...new TextEncoder().encode(text)];
    array = array.map(i => i.toString(16).padStart(2, "0"));
    return array.join(" ");
};
decode.hex = code => {
    let array = code.split(" ");
    array = array.map(i => parseInt(i, 16));
    array = Uint8Array.from(array);
    return new TextDecoder().decode(array);
};
```

## 2.2. CDN

我给 CLS 单独创建了一个[剪贴板](https://www.luogu.com.cn/paste/3zhbijww) 用于简化导入。

```js
eval((await (await fetch("/paste/3zhbijww?_contentOnly")).json()).currentData.paste.data)("00000001");
```

这样导入后会运行 `00000001` 剪贴板模块的内容。
