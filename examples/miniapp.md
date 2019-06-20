# 聊聊小程序

新来的 李其昌

---

## 目录

1. 简介
2. 小程序及页面生命周期
3. 自定义组件
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

据不完全统计（我知道的）

有以下这些：

---

<small>

**微信小程序**、苏宁小程序、**QQ 轻应用**、

**头条（抖音）小程序**、百度小程序、

阿里小程序（支付宝、淘宝、钉钉）、

快应用等

</small>

---

<small>

API 的设计及规范目前都以**微信小程序**为标准，

尽管各大平台都有自己的实现，但大思路基本**一致**。

</small>

---

所以...

---

接下来，我们以微信小程序为例

---

文件目录的基本结构

```js
├── pages/    // 所有的页面
├── components/ // 组件
├── assets/   // 资源文件
├── app.js    // 小程序入口文件
├── app.json  // 小程序配置文件
├── app.wxss  // 全局样式
├── project.config.json // 开发配置文件
├── sitemap.json  // 供微信搜索使用
```

---

app.json 文件

```json
{
  pages: [ "pages/index/index" ],
  window: {},
  tabBar: {
    list: [ { path: "pages/index/index" } ]
  },
  permission: {},
  sitemapLocation: "sitemap.json"
}
```

---

project.config.json 文件

```json
{
  setting: {},
  appid: "",
  condition: {
    miniprogram: [
      { pathName: ... }
    ]
  }
}
```

---

Page 基本组成

```js
├── pages/
│   ├── home/  // 首页
│   ├── ├── index.js     // 页面逻辑
│   ├── ├── index.wxml   // 页面布局
│   ├── ├── index.wxss   // 页面样式
│   ├── ├── index.json   // 页面配置
```

---

Component 基本组成

```js
├── components/
│   ├── banner/  // 轮播
│   ├── ├── index.js     // 组件逻辑
│   ├── ├── index.wxml   // 组件布局
│   ├── ├── index.wxss   // 组件样式
│   ├── ├── index.json   // 组件配置
```

---

模块化

<small>与 Common.js 的规范一致，采用 `exports` 与 `module.exports` 的方式**导出**，采用 `require` 的方式**引入**。</small>

---

### 小程序及页面生命周期

---

[App 的生命周期](https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/page.html)

| 属性 | 说明 |
| --- | --- |
| <small>onLaunch</small>  |  <small>监听小程序初始化</small>  |
| <small>onShow</small>   |  <small>监听小程序启动或切前台</small>   |
| <small>onHide</small> | <small>监听小程序切后台</small> |
| <small>onError</small> | <small>错误监听</small> |

---

[Page 的生命周期](https://res.wx.qq.com/wxdoc/dist/assets/img/page-lifecycle.2e646c86.png)

| 属性 | 说明 |
| --- | --- |
| <small>onLoad</small>  |  <small>监听页面加载</small>  |
| <small>onShow</small>   |  <small>监听页面显示</small>   |
| <small>onReady</small> | <small>初次渲染完成</small> |
| <small>onHide</small> | <small>监听页面隐藏</small> |
| <small>onUnload</small> | <small>监听页面卸载</small> |

---

### 自定义组件

---

原生组件，请看☞ [Docs](https://developers.weixin.qq.com/miniprogram/dev/component/)

---

DEMO 演示

---

组件中的相关字段：

1. properties 和 data
2. multipleSlots
3. externalClasses
4. methods - triggerEvent

---

### 神奇的 Button

---

Button 的坑点：

1. 自带样式
2. 只有 Button 有 open-type 属性 (非用不可)

---

被小游戏坑的小程序

[相关提示链接](https://developers.weixin.qq.com/blogdetail?action=get_post_info&lang=zh_CN&token=1650183953&docid=0000a26e1aca6012e896a517556c01)

---

[open-type](https://developers.weixin.qq.com/miniprogram/dev/component/button.html)

| 值 | 说明 |
| :---: | :---: |
| <small>share</small>  | <small>分享</small> |
| <small>getPhoneNumber</small>  | <small>获取手机号</small> |
| <small>getUserInfo</small> | <small>获取用户信息</small> |
| <small>openSetting</small> | <small>打开设置</small> |

---

分享

1. 实现 Page 中的 onShareAppMessage
2. 右上角转发
3. 按钮上添加 `open-type="share"`

> 注：右上角的转发可以隐藏

---

### 路由及本地存储

---

#### 路由

---

| 路由 | 说明 |
| :---: | :---: |
| <small>navigateTo</small>  | <small>保留当前，跳转新页面</small> |
| <small>navigateBack</small>  | <small>关闭当前，返回上级或多级</small> |
| <small>redirectTo</small> | <small>关闭当前，打开新页面</small>|
| <small>reLaunch</small> | <small>关闭所有，打开新页面</small> |
| <small>switchTab</small> | <small>切换 Tab</small> |

---

举个🌰

---

```js
wx.navigateTo({
  url: '/pages/about/index?a=10&b=10'
})
```

---

建议

```js
let qs = querystring({
  a: 10,
  b: 10
})
wx.navigateTo({
  url: `/pages/about/index?${qs}`
})
```

---

<small>如果可以，路径也不要自己写：</small>

```js
let qs = querystring({
  a: 10,
  b: 10
})
// 定义在全局
let index = '/pages/about/index'
wx.navigateTo({
  url: `${index}?${qs}`
})
```

---

[关于路由](https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/route.html)

---

#### 本地存储

---

Storage 存储

---

<small>每个微信小程序都可以有自己的本地缓存，可以通过 wx.setStorage/wx.setStorageSync、wx.getStorage/wx.getStorageSync、wx.clearStorage/wx.clearStorageSync，wx.removeStorage/wx.removeStorageSync 对本地缓存进行读写和清理。</small>

---

隔离策略

<small>同一个微信用户，同一个小程序 storage 上限为 10MB。storage 以用户维度隔离，同一台设备上，A 用户无法读取到 B 用户的数据；不同小程序之间也无法互相读写数据。</small>

---

文件存储 FileManager

---

FileManager 基本与 Node 一致

---

本地存储， 小程序限制 10 M

---

### Tips

---

1) 修改背景颜色

```css
page {
  background-color: #f2f2f2;
}
```

---

2) 如果遇到锚点滚动的需求，请使用 scroll-view

```html
<scroll-view scroll-into-view="{{toView}}">
</scroll-view>

<button bindtap="changeToView"></button>
```

---

3）image 有默认宽高

```css
image {
  width: 320px;
  height: 240px;
}
```

---

4）catchtap 与 bindtap

```html
<view bindtap="goDetail">
  <button catchtap="buy"></button>
</view>
```

---

5) 修改 appid

<small>不要直接修改 `project.confg.json`，在工具栏点击详情 -> appid -> 修改，否则不生效。</small>

---

6) 跳转其他小程序

<small>需在 app.json 中配置 `navigateToMiniProgramAppIdList` 字段</small>

---

7）定位需求

<small>必须加 `permission` 字段，否则审核可能会被拒。</small>

---

8）wx 的 API，可以 Promise 化

<small>可以自己封装一下，也可以用第三方的。</small>

---

9) 跨页面通讯

<small>1. 在 App 中声明 globalData，通过 getApp 获取</small>

<small>2. [Tencent/westore](https://github.com/Tencent/westore) - 当耐特</small>

---

### Q&A

---

More about me:

https://github.com/QC-L

Thanks
