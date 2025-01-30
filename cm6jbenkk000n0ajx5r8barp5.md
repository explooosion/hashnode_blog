---
title: "NPM - EPERM 錯誤"
seoTitle: "NPM - EPERM 錯誤"
seoDescription: "npm install fails on Windows with EPERM, operation not permitted error during rename"
datePublished: Wed Jul 27 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbenkk000n0ajx5r8barp5
slug: npm-eperm
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-27_NPM%20-%20EPERM%20%E9%8C%AF%E8%AA%A4/banner/1469631043_4456.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-27_NPM%20-%20EPERM%20%E9%8C%AF%E8%AA%A4/banner/1469631043_4456.png
tags: npm

---

npm install fails on Windows with "EPERM, operation not permitted" error during rename

npm install 無所不能，npm install  一招抓遍天下。（Ｘ

問題狀況
----

在 npm install 套件時，若出現 EPERM 錯誤，如下圖：

[![1469631043_4456.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-27_NPM%20-%20EPERM%20%E9%8C%AF%E8%AA%A4/1469631043_4456.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/0881dcfa-8c4d-4348-970d-77864832f12b/1469631043_4456.png)

可看到 Error: EPERM:  operration not permitted, rename .....

當初還搞不清以為什麼不支援系統之類的東東哈哈

還一度以為安裝的 [react-native-nav](https://www.npmjs.com/package/react-native-nav) 不支援 windows 等等

處理方式
----

在這邊我們只需要清除快取即可

```bash
npm cache clean
```

之後再重新，安裝套件

就可以看到啦～～～

```bash
npm install
```

![1469631209_31125.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-27_NPM%20-%20EPERM%20%E9%8C%AF%E8%AA%A4/1469631209_31125.png)

以上處理方式來源參考 Github： 

[npm install fails on Windows with "EPERM, operation not permitted" error during rename](https://github.com/Medium/phantomjs/issues/19)

有勘誤之處，不吝指教。ob'\_'ov