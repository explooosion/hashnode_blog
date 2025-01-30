---
title: "Node.js - nvm is not compatible with the npm config prefix（Mac ）"
seoTitle: "Node.js - nvm is not compatible with the npm config prefix（Mac ）"
seoDescription: "萌新的 Mac 使用者遇到的雜碎問題 ..."
datePublished: Fri Aug 31 2018 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbf8a0000809kw8qwnbst4
slug: nodejs-nvm-is-not-compatible-with-the-npm-config-prefixmac
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-08-31_Node.js%20-%20nvm%20is%20not%20compatible%20with%20the%20npm%20config%20prefix%EF%BC%88Mac%20%EF%BC%89/banner/1535724044_88918.jpg
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-08-31_Node.js%20-%20nvm%20is%20not%20compatible%20with%20the%20npm%20config%20prefix%EF%BC%88Mac%20%EF%BC%89/banner/1535724044_88918.jpg
tags: mac, yarn

---

萌新的 Mac 使用者遇到的雜碎問題 ...

最近開始上手 Mac，一瞬間變成電腦白痴。

本篇是在 Mac 安裝 Node.js 所遇到的奇秒問題。

[![1535724044_88918.jpg](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-08-31_Node.js%20-%20nvm%20is%20not%20compatible%20with%20the%20npm%20config%20prefix%EF%BC%88Mac%20%EF%BC%89/1535724044_88918.jpg)](https://dotblogsfile.blob.core.windows.net/user/incredible/7fc4e167-353b-4123-b353-29a1df490988/1535724044_88918.jpg)

當然在版本控管部分，

使用大家最熟悉的管理工具 [NVM](https://github.com/creationix/nvm)。

本篇記錄只有新手才會有的問題。

一、奇妙鐵板
------

安裝完畢後 ，在 vscode 中呼叫終端機時，

出現了以下奇景：

[![1535722261_72518.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-08-31_Node.js%20-%20nvm%20is%20not%20compatible%20with%20the%20npm%20config%20prefix%EF%BC%88Mac%20%EF%BC%89/1535722261_72518.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/7fc4e167-353b-4123-b353-29a1df490988/1535722261_72518.png)

訊息寫著：

```bash
nvm is not compatible with the npm config "prefix" option: currently set to "/usr/local"
Run `npm config delete prefix` or `nvm use --delete-prefix v8.10.0 --silent` to unset it.
```

結果試著照做：

```bash
npm config delete prefix
```

終端機重開後又發生一樣的問題。

在圖片中，可以看出筆者用 NVM 安裝 Node.js 的是 8.10.0。

但是使用：

```bash
node -v
# v10.9.0
```

居然不是我的版本！！！

這個可以算是控管上的衝突問題，

更悲劇的是，用盡全力 google，結果都是一樣的。

### 這時候仔細想想 ...

### yarn！？

[![1535724289_35567.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-08-31_Node.js%20-%20nvm%20is%20not%20compatible%20with%20the%20npm%20config%20prefix%EF%BC%88Mac%20%EF%BC%89/1535724289_35567.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/7fc4e167-353b-4123-b353-29a1df490988/1535724289_35567.png)

對！我有安裝。然後呢？

看一下官網：

[![1535722641_12808.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-08-31_Node.js%20-%20nvm%20is%20not%20compatible%20with%20the%20npm%20config%20prefix%EF%BC%88Mac%20%EF%BC%89/1535722641_12808.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/7fc4e167-353b-4123-b353-29a1df490988/1535722641_12808.png)

### 哦哦哦哦～～

### 啊啊啊啊～～

### 我當初下的指令是：

```bash
brew install yarn
```

知道問題了嗎？

安裝 yarn 的時候，也安裝到了 Node.js

我們版本控管是由 NVM，因此不可以被 yarn 蓋到。

二、解惑也  
 
---------

首先把 yarn 除掉，待會再重新安裝。

```bash
brew uninstall yarn
```

接著把 Node.js 移除，這葛版本是 yarn 所安裝的，

移除掉並不會影響到 NVM 所安裝的 Node.js。

```bash
brew uninstall node
```

這時候再次查詢版本：

```bash
node -v
# bash: /usr/local/bin/node: No such file or directory
```

別擔心那只是因為目前 NVM 不知道你要用哪個版本。

只要重新切換到指定版本即可：

```bash
nvm use 8.10.0
```

最後最後，別急！

我們要裝回原本的 yarn。

```bash
brew install yarn --without-node
```

重開終端幾，試試版本查詢～

看起來都很正常囉！！！

如果重開機發生以下問題：

```bash
env: node: No such file or directory
```

代表 NVM 預設的 Node.js 遺失了，

這時候只要指定預設版本即可（根據自己的版本）。

```bash
nvm alias default 8.10.0
```

記住這不是傳教。

[![1535724373_77344.jpeg](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-08-31_Node.js%20-%20nvm%20is%20not%20compatible%20with%20the%20npm%20config%20prefix%EF%BC%88Mac%20%EF%BC%89/1535724373_77344.jpeg)](https://dotblogsfile.blob.core.windows.net/user/incredible/7fc4e167-353b-4123-b353-29a1df490988/1535724373_77344.jpeg)

yarn，用心、誠心、寬心。

有勘誤之處，不吝指教。ob'\_'ov