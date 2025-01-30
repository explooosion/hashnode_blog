---
title: "Node.js - Install（nvm）"
seoTitle: "Node.js - Install（nvm）"
seoDescription: "node.js nvm 版本控制安裝之新手教學，新手上路。"
datePublished: Sun Jun 12 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbelz7000m0ajxahbq2ttl
slug: nodejs-installnvm
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-12_Node.js%20-%20Install%EF%BC%88nvm%EF%BC%89/banner/1465700322_33006.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-12_Node.js%20-%20Install%EF%BC%88nvm%EF%BC%89/banner/1465700322_33006.png

---

node.js nvm 版本控制安裝之新手教學，新手上路。

node.js 安裝方式有兩種，一種為直接從[官方網站](https://nodejs.org/en/)下載，進行一般安裝，

另一種進階安裝方法為透過**NVM** （Node.js 的版本控管軟體）進行安裝。

NVM 可隨時將 node.js 開發環境切換版本，而且透過 cmd 安裝 ...

較符合工程師 style ，好像也比較厲害 ? 哈哈

Downloads NVM
-------------

到 [nvm-windows](https://github.com/coreybutler/nvm-windows/releases) 下載安裝 nvm-setup.zip，

執行軟體並完成版控安裝。

USE NVM
-------

安裝完畢後開啟 cmd ，輸入 nvm，會列出基本功能命令。

```bash
nvm
```

[![1465700322_33006.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-12_Node.js%20-%20Install%EF%BC%88nvm%EF%BC%89/1465700322_33006.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/a41e3f3d-3389-4319-be67-126dc921e9b5/1465700322_33006.png)

接著我們輸入 nvm install latest ，安裝最新 node.js 版本

```bash
nvm install latest
```

[![1465700418_56618.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-12_Node.js%20-%20Install%EF%BC%88nvm%EF%BC%89/1465700418_56618.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/a41e3f3d-3389-4319-be67-126dc921e9b5/1465700418_56618.png)

若要安裝指定版本，則指定版本號即可

```bash
nvm install 4.2.2
```

[![1465701199_76368.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-12_Node.js%20-%20Install%EF%BC%88nvm%EF%BC%89/1465701199_76368.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/a41e3f3d-3389-4319-be67-126dc921e9b5/1465701199_76368.png)

若要移除指定版本，則使用 uninstall

```bash
nvm uninstall 4.2.2
```

![1465701265_29208.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-12_Node.js%20-%20Install%EF%BC%88nvm%EF%BC%89/1465701265_29208.png)

利用 nvm list 可查看當前已安裝的各版本，

\* 則為當前使用版本

```bash
nvm list
```

![1465701346_08576.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-12_Node.js%20-%20Install%EF%BC%88nvm%EF%BC%89/1465701346_08576.png)

若要切換或使用某版本，利用 nvm use \[version\] 即可

```bash
nvm use 4.2.2
```

![1465701405_12053.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-12_Node.js%20-%20Install%EF%BC%88nvm%EF%BC%89/1465701405_12053.png)

大功告成了~
------

接下還可以看其他應用 [Node.js - Express4](https://dotblogs.com.tw/explooosion/2016/06/11/213626)

有勘誤之處，不吝指教。ob'\_'ov