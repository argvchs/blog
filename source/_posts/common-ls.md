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

## 1.2. `require`

导入一个剪贴板模块，注意要在前面添加 `await` 因为返回的是一个 `Promise`。

```js
const mod = await require("00000001");
```

## 1.3. `require_cache`

`require` 的缓存，注意其类型为 [`Map`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map) 而不是 `Object`。

```js
// paste: 00000001
let x = 0;
exports.count = () => ++x;
```

```js
// paste: 00000002
console.log((await require("0bwumvaq")).count()); // output: 1
console.log((await require("0bwumvaq")).count()); // output: 2
console.log((await require("0bwumvaq")).count()); // output: 3

require_cache.delete("0bwumvaq");

console.log((await require("0bwumvaq")).count()); // output: 1
```

## 1.4. `module.exports`

导出模块。

```js
// paste: 00000001
module.exports = x => x * x;
```

```js
// paste: 00000002
const square = await require("00000001");
console.log(square(10)); // output: 100
```

## 1.5. `exports`

导出模块，但是和 `module.exports` 用法不同。

```js
// paste: 00000001
exports.square = x => x * x;
```

```js
// paste: 00000002
const mod = await require("00000001");
console.log(mod.square(10)); // output: 100
```

## 1.6. `encode` `decode`

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

你也可以自定义编码。

```js
encode.reverse = text => text.split("").reverse().join("");
decode.reverse = code => code.split("").reverse().join("");
```

## 1.7. 编码注释

`// encode <type>` 表示这个模块的内容的编码格式，若没有则为 `plain`。

```js
// paste: 00000001
// encode hex
// begin module
63 6f 6e 73 6f 6c 65 2e 6c 6f 67 28 22 48 65 6c 6c 6f 2c 20 57 6f 72 6c 64 21 22 29
// end module
```

```js
// paste: 00000002
require("00000001");
// output: Hello World!
```

## 1.8. 依赖注释

`// require <mod1> <mod2> ...` 表示当前模块依赖的剪贴板模块。

依赖注释只是标明模块的依赖。

## 1.9. `linker`

由于只有主站允许 `eval`，所以要在其他地方运行 CLS 必须要用 `linker` 预处理。

`linker` 返回的代码默认是不带返回值的，如果需要返回值可以在前面加上 `await`。

**`linker` 只会链接依赖注释中标明的依赖。**

```js
// paste: 00000001
// begin module
exports.square = x => x * x;
// end module
```

```js
// paste: 00000002
// require 00000001
// begin module
const mod = await require("00000001");
exports.cube = x => x * mod.square(x);
// end module
```

```js
console.log(await linker("00000002"));
/*
output (formatted):

(async () => {
    const _linked_modules = new Map();

    _linked_modules.set("00000002", async () => {
        const module = { exports: {} };
        await (async (exports, module) => {
            const mod = await require("00000001");
            exports.cube = x => x * mod.square(x);
        })(module.exports, module);
        return module.exports;
    });

    _linked_modules.set("00000001", async () => {
        const module = { exports: {} };
        await (async (exports, module) => {
            exports.square = x => x * x;
        })(module.exports, module);
        return module.exports;
    });

    const require_cache = new Map();
    const require = async url => {
        if (!_linked_modules.has(url)) throw Error(`Cannot find module '${url}'`);
        let flag;
        await navigator.locks.request("require_cache", async () => {
            flag = require_cache.has(url);
            if (!flag) require_cache.set(url);
        });
        if (flag) return require_cache.get(url);
        let result = await _linked_modules.get(url)();
        require_cache.set(url, result);
        return result;
    };
    return require("00000002");
})();
*/
```

# 2. 运行

## 2.1. Polyfill

将 CLS Polyfill 放到顶层模块代码的前面就可以了。

```js
const _async_function = (async () => {}).constructor;
const _reg1 = /^\s*\/\/\s*begin\s+module\s*$((.|\n)*)^\s*\/\/\s*end\s+module\s*$/m;
const _reg2 = /^\s*\/\/\s*encode\s+(\w+)\s*$/m;
const _reg3 = /^\s*\/\/\s*require((\s+\w+)*)\s*$/m;

const encode = {};
const decode = {};
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

const require_cache = new Map();
const require = async url => {
    let flag;
    await navigator.locks.request("require_cache", async () => {
        flag = require_cache.has(url);
        if (!flag) require_cache.set(url);
    });
    if (flag) return require_cache.get(url);
    let response = await fetch(`/paste/${url}?_contentOnly`);
    let json = await response.json();
    let data = json.currentData.paste.data;
    let source = data.match(_reg1)?.[1] || data;
    let encode = data.match(_reg2)?.[1] || "plain";
    let result = await (async () => {
        const module = { exports: {} };
        await _async_function("exports", "module", decode[encode](source))(module.exports, module);
        return module.exports;
    })();
    require_cache.set(url, result);
    return result;
};

const linker = async url => {
    let result = `
    (async () => {
        const _linked_modules = new Map();
    `;
    const impl_cache = new Set();
    const impl = async url => {
        let flag;
        await navigator.locks.request("linker_impl_cache", async () => {
            flag = impl_cache.has(url);
            if (!flag) impl_cache.add(url);
        });
        if (flag) return;
        let response = await fetch(`/paste/${url}?_contentOnly`);
        let json = await response.json();
        let data = json.currentData.paste.data;
        let source = data.match(_reg1)?.[1] || data;
        let encode = data.match(_reg2)?.[1] || "plain";
        let module = data.match(_reg3)?.[1] || "";
        result += `
        _linked_modules.set("${url}", async () => {
            const module = { exports: {} };
            await (async (exports, module) => {
                ${decode[encode](source)}
            })(module.exports, module);
            return module.exports;
        });
        `;
        module = module.trim();
        if (module !== "") await Promise.all(module.split(/\s+/).map(impl));
    };
    await impl(url);
    result += `
        const require_cache = new Map();
        const require = async url => {
            if (!_linked_modules.has(url)) throw Error(\`Cannot find module '\${url}'\`);
            let flag;
            await navigator.locks.request("require_cache", async () => {
                flag = require_cache.has(url);
                if (!flag) require_cache.set(url);
            });
            if (flag) return require_cache.get(url);
            let result = await _linked_modules.get(url)();
            require_cache.set(url, result);
            return result;
        };
        return require("${url}");
    })();
    `;
    return result;
};
```

## 2.2. CDN

我给 CLS 单独创建了一个[剪贴板](https://www.luogu.com.cn/paste/3zhbijww) 用于简化运行过程。

```js
await eval((await (await fetch("/paste/3zhbijww?_contentOnly")).json()).currentData.paste.data)("00000001");
```

这样会运行 `00000001` 剪贴板模块的内容。

## 2.3. 预处理

先用上述的 `linker` 预处理，这样就可以直接运行了。

如果觉得预处理之后体积太大可以用 [Terser](https://try.terser.org) 压缩一下。
