---
title: "Node.js - Express4"
seoTitle: "Node.js - Express4"
seoDescription: "node.js express 環境安裝之新手教學，請安心服用。"
datePublished: Sat Jun 11 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbellh000l0ajxdkwbh7aa
slug: nodejs-express4
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-11_Node.js%20-%20Express4/banner/1465650931_90659.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-11_Node.js%20-%20Express4/banner/1465650931_90659.png
tags: express

---

node.js express 環境安裝之新手教學，請安心服用。

Node.js 有許多快速開發的框架，常見如 express、koa 等，

本篇簡單幾個步驟，帶著大家建立 express framework 下的網頁。

 框架安裝
-----

express 全域安裝，安裝完畢後可看見版本號 4.13.1。

```bash
npm install -g express-generator@4
```

[![1465650931_90659.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-11_Node.js%20-%20Express4/1465650931_90659.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/f0bb4f91-b6fa-4b35-803b-fef89496aa2f/1465650931_90659.png)

框架指令
----

express 本身有些內建指令，利用 express -V 可查詢版本。

```bash
express -V
```

![1465651072_33937.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-11_Node.js%20-%20Express4/1465651072_33937.png)

利用 express -h 可提供指令說明。

```bash
express -h
```

[![1465651267_67317.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-11_Node.js%20-%20Express4/1465651267_67317.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/f0bb4f91-b6fa-4b35-803b-fef89496aa2f/1465651267_67317.png)

專案建立
----

建立專案 express -e \[ 專案名稱 \]

```bash
express -e express-demo
```

[![1465651487_27197.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-11_Node.js%20-%20Express4/1465651487_27197.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/f0bb4f91-b6fa-4b35-803b-fef89496aa2f/1465651487_27197.png)

完成後最下方有提示安裝及執行，

我們先進入剛剛建立的專案資料夾，並進行初始化。

```bash
cd express-demo
npm install
```

[![1465651646_12112.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-11_Node.js%20-%20Express4/1465651646_12112.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/f0bb4f91-b6fa-4b35-803b-fef89496aa2f/1465651646_12112.png)

專案執行
----

完成安裝建置後，我們即可執行

```bash
npm start
```

[![1465651964_05368.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-11_Node.js%20-%20Express4/1465651964_05368.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/f0bb4f91-b6fa-4b35-803b-fef89496aa2f/1465651964_05368.png)

此指令可於 package.json - scripts 進行查看修改

![1465651800_3369.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-11_Node.js%20-%20Express4/1465651800_3369.png)

執行畫面
----

npm start 執行後預設為 3000 port，進入 [http://localhost:3000/](http://localhost:3000/)

看見歡迎畫面，就算大功告成啦 ~~ (๑˘ ₃˘๑) 

[![1465652121_86239.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-11_Node.js%20-%20Express4/1465652121_86239.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/f0bb4f91-b6fa-4b35-803b-fef89496aa2f/1465652121_86239.png)

有勘誤之處，不吝指教。ob'\_'ov