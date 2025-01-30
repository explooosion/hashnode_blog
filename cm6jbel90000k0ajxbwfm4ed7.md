---
title: "Node.js - fs.renameSync"
seoTitle: "Node.js - fs.renameSync"
seoDescription: "node.js 檔案上傳 fs 寫入問題，請安心服用。"
datePublished: Sun Jun 05 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbel90000k0ajxbwfm4ed7
slug: nodejs-fsrenamesync
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-05_Node.js%20-%20fs.renameSync/banner/1465104406_70045.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-05_Node.js%20-%20fs.renameSync/banner/1465104406_70045.png
tags: stream

---

node.js 檔案上傳 fs 寫入問題，請安心服用。

前言說明

本篇為練習實作 [Node入門](http://www.nodebeginner.org/index-zh-tw.html) 發生的問題。

本魔法實習生花了一個晚上，

尋找為何 node.js 在 upload file 應用上會發生錯誤**「cross-device」**。

[![1465104406_70045.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-05_Node.js%20-%20fs.renameSync/1465104406_70045.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/a8de619c-6332-4140-8afb-be7d4219b882/1465104406_70045.png)

檔案上傳時，會存於 c: ... Local\\Temp 暫存資料夾，

若指定實體存放路徑為**別的磁碟槽**時，會發生**存取權限失效**，

因此，本篇介紹調用 util，將檔案 clone 至別分區，在進行 unlink。

引用檔案
----

```javascript hljs
var util = require('util');
```

修改 renameSync
-------------

原本程式碼：

```javascript hljs
fs.renameSync(files.upload.path, "C:/tmp/test.png");
```

建立 ReadStream，來源請指定剛上傳的檔案。

```javascript hljs
var readStream = fs.createReadStream(files.upload.path);
```

建立 WriteStream，指定檔案寫入存放的路徑（預設位置為 createServer 所在位置）。

```javascript hljs
var writeSteam = fs.createWriteStream("/tmp/test.png");
```

最後利用剛剛引用的 util ，將檔案寫入並將 fs unlinkSync。

```javascript hljs
util.pump(readStream, writeSteam, function() {
            fs.unlinkSync(files.upload.path);
        });
```

完整程式碼

```javascript hljs
var fs = require("fs"),
    formidable = require("formidable");

var util = require('util');


function upload(response, request) {
    console.log("Request handler 'upload' was called.");

    var form = new formidable.IncomingForm();
    console.log("about to parse");
    form.parse(request, function(error, fields, files) {
        console.log("parsing done");
        //fs.renameSync(files.upload.path, "C:/tmp/test.png");

        var readStream = fs.createReadStream(files.upload.path);
        var writeSteam = fs.createWriteStream("/tmp/test.png");

        util.pump(readStream, writeSteam, function() {
            fs.unlinkSync(files.upload.path);
        });


        response.writeHead(200, { "Content-Type": "text/html" });
        response.write("received image:<br/>");
        response.write("<img src='/show' />");
        response.end();
    });
}
```

參考資料
----

[【已解决】Node.js中所用的fs.renameSync出错：Error: EXDEV, cross-device link not permitted](http://www.crifan.com/node_js_use_fs_renamesync_error_exdev_cross_device_link_not_permitted/)

有勘誤之處，不吝指教。ob'\_'ov