---
title: "Gulp - 入門教學"
seoTitle: "Gulp - 入門教學"
seoDescription: "前端的自動化佈署工具有許多，本篇介紹熱門的 gulp.js，來提升工作效率吧！"
datePublished: Sun Apr 30 2017 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jberwx000k09jv8wwr21cj
slug: gulp
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-04-30_Gulp%20-%20%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8/banner/1493548375_11121.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-04-30_Gulp%20-%20%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8/banner/1493548375_11121.png
tags: gulp

---

前端的自動化佈署工具有許多，本篇介紹熱門的 gulp.js，來提升工作效率吧！

一、前言
----

在前端的開發過程中，當檔案要發佈的時候，總會進行一些批次的處理，

又或者監控檔案、程式碼編譯等等，諸如：

1.  LESS、SASS、SCSS 、 Stylus 編譯。
2.  JavaScript Template 編譯。
3.  JS、CSS 檔案前綴處理。
4.  差異化抽取檔案。
5.  程式碼混淆、打包。

目前較熱門的有 [**Grunt**](https://gruntjs.com/)、**[Gulp](http://gulpjs.com/)**，本文將介紹 gulp 的安裝以及使用方法。

二、Gulp安裝
--------

gulp 必須透過 [npm](https://www.npmjs.com/) 下載，請務必先安裝好 [node.js](https://nodejs.org/en/) 唷！

首先進行全域安裝 gulp，如此一來才能使用 gulp 指令。

```bash
npm install --global gulp
```

緊接著在當前專案底下安裝 gulp。

```bash
npm install gulp
```

版本目前是 3.9.1。

```bash
npm list gulp
```

![1493548375_11121.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-04-30_Gulp%20-%20%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8/1493548375_11121.png)

三、程式碼撰寫
-------

新增檔案 ，然後引用 gulp，

task 是一個任務的建立，hello 則為任務名稱。

gulpfile.js

```javascript
const gulp = require('gulp');
 
gulp.task('hello', function(){
	console.log('Hello Gulp.js');
});
```

四、執行任務
------

當我們要執行指定的任務時，直接 gulp \[任務名稱\] 即可。

```bash
gulp hello
```

可以看到 cmd 輸出，任務的開始與結束，

而其中我們寫的 console.log 也會被印出來。  
[![1493548723_27684.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-04-30_Gulp%20-%20%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8/1493548723_27684.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/86d32af2-8813-47c6-9df8-4aca2fda8438/1493548723_27684.png)

五、延伸套件
------

而通常我們在使用 gulp 的時候，都會安裝一些常用的套件，

接下來會教大家使用一些常用的套件。

1.  gulp-jshint
2.  gulp-uglify
3.  gulp-concat

### **【[gulp-jshint](https://github.com/spalger/gulp-jshint)】－檢查 JavaScript 語法**

[jshint](http://jshint.com/install/) 提供對於 JavaScript 的語法檢查，在使用此之前，要先安裝其原本的套件。

```bash
npm install jshint
```

之後才可以安裝基於 jshint 所延伸過來的 gulp-jshint。

```bash
npm install gulp-jshint
```

如果只有安裝 gulp-jshint，而其仰賴的 jshint 沒安裝的話，也不用擔心，

在安裝的時候 npm 會提醒使用者。

![1493549259_28738.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-04-30_Gulp%20-%20%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8/1493549259_28738.png)

目前的 jshint 版本為 2.9.4。

![1493549517_23416.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-04-30_Gulp%20-%20%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8/1493549517_23416.png)

首先我們先任意建立一個 js 檔案，待會可以做為檢查測試用。

我們都知道在 ES6 中， const 為常數，不可重複定義其值，因此下方的範例將是錯誤的。

test.js

```javascript
const a = 1;
a = 2;
```

gulpfile.js

```javascript
const gulp = require('gulp'),
    jshint = require('gulp-jshint');

gulp.task('check', function () {
    gulp.src('test.js')
        .pipe(jshint())
        .pipe(jshint.reporter())
    console.log('check done.');
});
```

上述引用了 gulp-jshint，在下方我們利用 gulp.src 來表示來源路徑，

*   .pipe(jshint())：執行檢查
*   .pipe(jshint.reporter())： 將結果印出

執行檢查 

```javascript
gulp check
```

 系統回報兩個錯誤 2errors：

*   line1 ：回報我們 const 是 ES6 用法（但會將其歸類為 error），是不該出現的。
*   line2：要被覆寫的 a 屬於常數，是該出現的。

[![1493550847_5034.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-04-30_Gulp%20-%20%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8/1493550847_5034.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/86d32af2-8813-47c6-9df8-4aca2fda8438/1493550847_5034.png)

 jshint 版本 2.9.4 對於 ES6 需要另外宣告 esnext，可以從[官方](http://jshint.com/docs/options/)得知該消息。

[![1493550932_13275.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-04-30_Gulp%20-%20%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8/1493550932_13275.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/86d32af2-8813-47c6-9df8-4aca2fda8438/1493550932_13275.png)

因次我們修正一下程式碼：

gulpfile.js

```javascript
gulp.task('check', function () {
    gulp.src('test.js')
        .pipe(jshint({
            esnext: true
        }))
        .pipe(jshint.reporter())
    console.log('check done.');
});
```

將 jshint 加上參數 esnext：true 就能夠處理，如此一來就可以用來檢查 JS 囉！

[![1493551001_99048.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-04-30_Gulp%20-%20%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8/1493551001_99048.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/86d32af2-8813-47c6-9df8-4aca2fda8438/1493551001_99048.png)

### **【[gulp-uglify​](https://github.com/terinjokes/gulp-uglify)】－JavaScript 程式碼壓縮混淆**

能夠使程式碼壓縮，或是將程式碼混淆。

目前不支援 ES6，如果要針對 ES6，建議先透過 [gulp-babel](https://github.com/babel/gulp-babel) 轉換為 ES5

安裝 gulp-uglify 套件。

```bash
npm install gulp-uglify
```

任意建立 js 檔案。

test.js

```javascript
var a = 1, b = 2, c = 3;
var d = a * b * c + a;
console.log(d);
```

gulpfile.js

```javascript
const gulp = require('gulp'),
    uglify = require('gulp-uglify');

gulp.task('uglify', function () {
    gulp.src('test.js')
        .pipe(uglify())
        .pipe(gulp.dest('dist'))
});
```

*   gulp.dest 為輸出目的之資料夾

執行結果

```bash
gulp uglify
```

![1493552548_7916.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-04-30_Gulp%20-%20%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8/1493552548_7916.png)

### **【[gulp-](https://github.com/terinjokes/gulp-uglify)[concat](https://github.com/contra/gulp-concat)[​](https://github.com/terinjokes/gulp-uglify)】－程式碼打包**

簡單就是將多個檔案合併成一支囉！

安裝 gulp-concat。

```bash
npm install gulp-concat
```

以下範例將 test.js 與 test2.js 進行打包

test.js

```javascript
/**
 * This is test.js
 */
console.log('test');
```

test2.js

```javascript
/**
 * This is test2.js
 */
console.log('test2');
```

gulpfile.js

```javascript
const gulp = require('gulp'),
    concat = require('gulp-concat');

gulp.task('concat', function () {
    gulp.src('js/*.js')
        .pipe(concat('bundle.js'))
        .pipe(gulp.dest('dist'))
});
```

*   gulp.src：來源為 js 資料夾底下所有的 js檔案。
*   concat：打包後的檔名為 bundle.js
*   gulp.dest：輸出到 dist 資料夾中

執行結果：

```bash
gulp concat
```

[![1493553163_66702.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-04-30_Gulp%20-%20%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8/1493553163_66702.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/86d32af2-8813-47c6-9df8-4aca2fda8438/1493553163_66702.png)[![1493553323_05416.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-04-30_Gulp%20-%20%E5%85%A5%E9%96%80%E6%95%99%E5%AD%B8/1493553323_05416.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/86d32af2-8813-47c6-9df8-4aca2fda8438/1493553323_05416.png)

六、後記
----

對於前端的自動化佈署，如何加快開發的腳步是十分重要的，

本篇針對 gulp 僅提供簡單安裝使用，更多的套件延伸應用將在下一篇提到，

如何即時監控檔案、編譯樣式SASS、差異備份等等......。

因為內容太多惹 rrrr

參考資料：

[gulp 中的增量编译 - 韩子迟 - 博客园](http://www.cnblogs.com/zichi/p/6265208.html)

[Gulp：任务自动管理工具 -- JavaScript 标准参考教程（alpha）](http://javascript.ruanyifeng.com/tool/gulp.html)

有勘誤之處，不吝指教。ob'\_'ov