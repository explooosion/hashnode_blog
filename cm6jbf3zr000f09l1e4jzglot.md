---
title: "React.js - dva 多麼麻煩的 sass 引入步驟"
seoTitle: "React.js - dva 多麼麻煩的 sass 引入步驟"
seoDescription: "如果你也很不爽官方對於 sass 的 issue ..."
datePublished: Sat Jun 02 2018 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbf3zr000f09l1e4jzglot
slug: reactjs-dva-sass
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-06-02_React.js%20-%20dva%20%E5%A4%9A%E9%BA%BC%E9%BA%BB%E7%85%A9%E7%9A%84%20sass%20%E5%BC%95%E5%85%A5%E6%AD%A5%E9%A9%9F/banner/1527926407_20427.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-06-02_React.js%20-%20dva%20%E5%A4%9A%E9%BA%BC%E9%BA%BB%E7%85%A9%E7%9A%84%20sass%20%E5%BC%95%E5%85%A5%E6%AD%A5%E9%A9%9F/banner/1527926407_20427.png
tags: sass, scss

---

如果你也很不爽官方對於 sass 的 issue ...

最近因為熟悉 [hyperapp](https://github.com/hyperapp/hyperapp) 後，

因為專案的需要而回頭使用以前的 [dvajs/dva](https://github.com/dvajs/dva) 框架，

真的覺得先熟悉 hyperapp 是對的，

再回來看看會發現更好懂呢 ~

一、前言
----

因為沒有 sass、scss 真的很難寫 css 樣式，

都得要寫成一拖拉庫，不能寫成巢狀。

為了在 dva 內使用 scss，搞了一堆時間，

對於官方的態度，更是不爽 😡，

一堆 issue，回答的卻沒能幫助到。

例如：[sass配置 为什么引入的时候还是报错没有配置 #1440](https://github.com/dvajs/dva/issues/1440)

結果只有這樣回應：

[![1527926407_20427.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-06-02_React.js%20-%20dva%20%E5%A4%9A%E9%BA%BC%E9%BA%BB%E7%85%A9%E7%9A%84%20sass%20%E5%BC%95%E5%85%A5%E6%AD%A5%E9%A9%9F/1527926407_20427.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/f9f75df9-adf5-48f2-aed3-d245ae5ea6b4/1527926407_20427.png)

然後點進去 [roadhog#sass](https://github.com/sorrycc/roadhog#sass) 看也只有這樣說明：

[![1527926469_5227.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-06-02_React.js%20-%20dva%20%E5%A4%9A%E9%BA%BC%E9%BA%BB%E7%85%A9%E7%9A%84%20sass%20%E5%BC%95%E5%85%A5%E6%AD%A5%E9%A9%9F/1527926469_5227.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/f9f75df9-adf5-48f2-aed3-d245ae5ea6b4/1527926469_5227.png)

🤬！！！，根本把問題丟回給 node-sass - [sass/node-sass#options](https://github.com/sass/node-sass#options) 

二、作法
----

研究了好久，終於猜出，roadhog 原本就把 less 包進去，

所以可以很自然地使用。

原理其實就是掃描 node-modules 的時候會包進去：

所以只要一行就可以解決：

```bash
npm install node-sass sass-loader --save
```

*   不需要修改本地任何檔案的配置
*   不需要新增任何指令
*   安裝時請雙手放空

安裝完後，只要把副檔名改成 .scss

然後引入的時候改成 scss 就可：

```javascript
import './index.scss'
```
```javascript
import styles from './IndexPage.scss'
```

就完成了！！！！！！

#### **他媽的為什麼官方不補上去說明？**

有勘誤之處，不吝指教。ob'\_'ov