# 聊聊小程序

新来的 李其昌

---

## 目录

1. 简介
2. 小程序及页面生命周期
3. 原生组件及自定义组件
4. 神奇的 Button
5. 路由及本地存储
6. Tips

---

### 简介

---

什么是小程序？

---

小程序是**业务形态**，并不是~技术形态~。

---

目前有哪些小程序？

---

据不完全统计（我知道的）有以下这些：

**微信小程序**、苏宁小程序、**QQ 轻应用**、

**头条（抖音）小程序**、百度小程序、

阿里小程序（支付宝、淘宝、钉钉）、

快应用等

---

API 的设计及规范目前都以**微信小程序**为标准，

尽管各大平台都有自己的实现，但大思路基本**一致**。

---

所以...

---

接下来，我们以微信小程序为例

---

```html
├── pages/
├── config/
├── components/
├── assets/
├── app.js
├── app.json
├── app.wxss
├── project.config.json
├── sitemap.json
```

---

### Use in Template

```html
<template>
  <MarkDisplay markdown="..." />
</template>
```

---

You can use [Markdown](https://commonmark.org/help/) to write slides.

For example:

---

# Heading 1

## Heading 2

### Heading 3

paragraph

---

### Table

| Foo | Bar | Baz |
| --- | --- | --- |
| 1   | 2   | 3   |
| 4   | 5   | 6   |

---

You can also do some extensions by your own:

---

1) set your code highlighted

```js
export default {
  data() {
    return {
      msg: "Highlighted!"
    };
  }
};
```

---

2) or support touch events

Try to **SWIPE horizontally** on the touch screen.

---

<!-- style: color: blue; font-family: monospace; -->

3) custom background using meta syntax

`<!-- style: color: blue; font-family: monospace; -->`

---

4) reset base url

```html
<MarkDisplay
  ...
  baseUrl="https://github.com/"
/>
```

![](./favicon.ico) this is the `./favicon.ico`

---

At almost the end:

You can press **<kbd>⌘+P</kbd>** to print your slides into PDF.

<small>you can have a try _now_</small>

---

More about me:

https://github.com/jinjiang/vue-mark-display

Thanks
