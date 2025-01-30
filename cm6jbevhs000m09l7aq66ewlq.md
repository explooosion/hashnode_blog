---
title: "Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［2］環境建置的前哨"
seoTitle: "Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［2］環境建置的前哨"
seoDescription: "記錄著從 Vue 新手村出發的練功歷程..."
datePublished: Fri Jul 28 2017 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbevhs000m09l7aq66ewlq
slug: vuejs-20-vue-2
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB2%EF%BC%BD%E7%92%B0%E5%A2%83%E5%BB%BA%E7%BD%AE%E7%9A%84%E5%89%8D%E5%93%A8/banner/1501225003_87954.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB2%EF%BC%BD%E7%92%B0%E5%A2%83%E5%BB%BA%E7%BD%AE%E7%9A%84%E5%89%8D%E5%93%A8/banner/1501225003_87954.png
tags: vue

---

記錄著從 Vue 新手村出發的練功歷程...

本篇任務指引：
-------

1.  認識魔法陣
2.  使用 Vue 寫出 HelloWorld

**一、咕嚕咕嚕魔法陣**
-------------

首先要了解 Vue 的環境基本組成，

在這之前先預判，可能你已經聽過 [vue-cli](https://github.com/vuejs/vue-cli)、[vuex](https://github.com/vuejs/vuex)...等等，

但無論如何，使用這類快速指令或框架之前，總得要會最基本的使用方式，

因此將從最簡單的使用方式講起。

首先這是我們常見的網頁基本架構：

![1501225003_87954.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB2%EF%BC%BD%E7%92%B0%E5%A2%83%E5%BB%BA%E7%BD%AE%E7%9A%84%E5%89%8D%E5%93%A8/1501225003_87954.png)

到了 Vue 其實也是以相似的架構進行，

由於網頁是由上往下讀取，因此會在末端下方插入 script，進行 DOM 的操作。

![1501225429_07277.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB2%EF%BC%BD%E7%92%B0%E5%A2%83%E5%BB%BA%E7%BD%AE%E7%9A%84%E5%89%8D%E5%93%A8/1501225429_07277.png)

在寫之前我們會將 vue.js 引入：

可以使用官方範例所使用的：

```html
<script src="https://unpkg.com/vue"></script>
```

也可以使用 [CDN](https://zh.wikipedia.org/wiki/%E5%85%A7%E5%AE%B9%E5%82%B3%E9%81%9E%E7%B6%B2%E8%B7%AF)： 

```html
<script src='https://cdnjs.cloudflare.com/ajax/libs/vue/2.4.2/vue.js'></script>
```

[![1501225398_01499.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB2%EF%BC%BD%E7%92%B0%E5%A2%83%E5%BB%BA%E7%BD%AE%E7%9A%84%E5%89%8D%E5%93%A8/1501225398_01499.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/6724494e-39d0-4246-afc4-177d7b591207/1501225398_01499.png)

以上就是最基本的環境配置結構，很好理解吧！

![1501225487_20991.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB2%EF%BC%BD%E7%92%B0%E5%A2%83%E5%BB%BA%E7%BD%AE%E7%9A%84%E5%89%8D%E5%93%A8/1501225487_20991.png)

**二、建立第一個魔法陣**
--------------

在範例的內容中，程式碼只顯示 body 的內容，別忘了 head 要引入 vue.js 哦

```html
<script src='https://cdnjs.cloudflare.com/ajax/libs/vue/2.4.2/vue.js'></script>
```

我們試著利用 Vue.js 寫出 HelloWorld：

```html
<body>

    <div id="hello">
        {{ msg }}
    </div>
    <script>
        new Vue({
            el: '#hello',
            data: {
                msg: 'Hello World !'
            }
        });
    </script>
</body>
```

打開網頁看結果就可以看到：

![1501226951_66727.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB2%EF%BC%BD%E7%92%B0%E5%A2%83%E5%BB%BA%E7%BD%AE%E7%9A%84%E5%89%8D%E5%93%A8/1501226951_66727.png)

首先 el 原本名稱其實是 [element](https://developer.mozilla.org/zh-TW/docs/Web/HTML/Element)，表示你想要綁定哪個網頁元件，做為根組件，

什麼意思？如下圖紅框處：

![1501227130_29854.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB2%EF%BC%BD%E7%92%B0%E5%A2%83%E5%BB%BA%E7%BD%AE%E7%9A%84%E5%89%8D%E5%93%A8/1501227130_29854.png)

我們決定源頭根的來源是 #hello，

用「＃」表示要尋找的依據是 id，

```javascript
el: '#hello'
```

如果今天想找 class 為 hello 的就是用「.」：

```javascript
el: '.hello'
```

所以今天只要在 id 為 hello 的元件中塞入任何東西，

通通都會受到根組件的控制，像是下方範例的 label，通通都可以被根組件控制。

```html
<div id="hello">
 {{ msg }}
 <label>葡萄1<label>
 <label>葡萄2<label>
</div>
```

那剛剛的 data 是什麼呢？

```javascript
data: {
   msg: 'Hello World !'
}
```

data 可以用來儲存我們的資料，你也可以放陣列：

```javascript
data: {
   msg: 'Hello World !',
   arr: [1,2,3] 
}
```

因此我們有了一個變數 msg，其值為一個字串 'Hello World !'，

最後如果我們想要取出他讓它渲染在畫面上，只要利用兩個大括弧 {{ }} 就可以做到：

```html
<div id="hello">
    {{ msg }}
</div>
```

**三、強化你的魔法陣**
-------------

經過上述的範例，請試著將下方改以 vue 方式渲染資料，

在 label 中的文字請改成 data 的方式綁定：

```html
<div id="hello">
 {{ msg }}
 <label>葡萄1<label>
 <label>葡萄2<label>
</div>
```

首先開始畫陣，進行等價交換！

[![1501227992_05444.jpg](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB2%EF%BC%BD%E7%92%B0%E5%A2%83%E5%BB%BA%E7%BD%AE%E7%9A%84%E5%89%8D%E5%93%A8/1501227992_05444.jpg)](http://ciyuanfan.baidu.com/news/get?id=149449129747376905)

欸不對，臭 87。

只要修改一下剛剛的程式就可做到，

在 data 內新增變數，用來存放此兩個字串：

```javascript
data: {
   msg: 'Hello World !',
   grapes1: '葡萄1',
   grapes2: '葡萄2',
}
```

再將剛剛 label 的內容改為 {{ }} 方式綁定即可：

```html
<div id="hello">
 {{ msg }}
 <label>{{ grapes1 }}<label>
 <label>{{ grapes2 }}<label>
</div>
```

完整程式碼：

```html
<body>

    <div id="hello">
        {{ msg }}
        <label>{{ grapes1 }}</label>
        <label>{{ grapes2 }}</label>
    </div>
    <script>
        new Vue({
            el: '#hello',
            data: {
                msg: 'Hello World !',
                grapes1: '葡萄1',
                grapes2: '葡萄2',
            }
        });
    </script>
</body>
```

畫面結果：_（雖然畫面有點醜）_

![1501228504_68898.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB2%EF%BC%BD%E7%92%B0%E5%A2%83%E5%BB%BA%E7%BD%AE%E7%9A%84%E5%89%8D%E5%93%A8/1501228504_68898.png)

以上本次任務了解到，

如何綁定根組件，並且進行資料的渲染！

### Next Stop：

### [Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［3］資料綁定的表單](https://dotblogs.com.tw/explooosion/2017/07/29/215127)

有勘誤之處，不吝指教。ob'\_'ov