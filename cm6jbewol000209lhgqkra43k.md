---
title: "Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［5］起死回生過濾器"
seoTitle: "Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［5］起死回生過濾器"
seoDescription: "記錄著從 Vue 新手村出發的練功歷程..."
datePublished: Wed Aug 02 2017 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbewol000209lhgqkra43k
slug: vuejs-20-vue-5
tags: vue

---

記錄著從 Vue 新手村出發的練功歷程...

本篇任務指引：
-------

1.  得知過濾器已死的消息（Q）
2.  獲得自訂過濾器的能力（F）

今天想要紀錄的是 Filter，首先我們先聆聽「蕭邦－夜曲」默哀一下：

為何標題要下得如此可怕呢？

在 Vue 1.x 版本的時候，我們可以使用模組內提供的過濾器（Filter）。

何謂過濾器？

如果使用過 [Angular](https://angular.io/) 的朋友應該對 Pipe 很熟悉，

透過簡單的語法就可以將我們指定的值進行格式化，

例如字母大小寫、金錢格式轉換等等。

簡單來說，就是把內容轉成我們希望的樣貌：

![filter.gif](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-08-02_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB5%EF%BC%BD%E8%B5%B7%E6%AD%BB%E5%9B%9E%E7%94%9F%E9%81%8E%E6%BF%BE%E5%99%A8/filter.gif)

*   圖片來源：[Chatterfall Gifs](https://rene-henrich.de/animation/chatterfall-introduction-animations#animation/chatterfall-introduction-animations-headline)

### ［回顧歷史］

以下為 Vue 1.x 簡單的範例：

注意：以下範例僅能在 Vue 1.x 版本

首先請載入 Vue 1.x。

```html
<script src='https://cdnjs.cloudflare.com/ajax/libs/vue/1.0.28-csp/vue.js'></script>
```

撰寫程式碼 。

```html
<h1>VueJS - Filter</h1>

<div class="filter">
    <h3>
        {{letter}} -> {{ letter | uppercase }}
    </h3>
    <h3>
        {{money}} -> {{ money | currency }}
    </h3>
</div>

<script>
    new Vue({
        el: '.filter',
        data: {
            letter: 'abc',
            money: 9487
        },
    });
</script>
```

實際畫面：

![1501668372_89431.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-08-02_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB5%EF%BC%BD%E8%B5%B7%E6%AD%BB%E5%9B%9E%E7%94%9F%E9%81%8E%E6%BF%BE%E5%99%A8/1501668372_89431.png)

回顧上述程式碼，我們可以看到有一段奇怪的寫法：

```html
{{ letter | uppercase }}
```

我們可以得知，letter 是 data 中的變數，

而利用「|」加上指定的格式，就可以將左側的值更改為經過格式化的值，

「uppercase 」為內建的過濾器保留字，即為轉成大寫字母。

如此方便的過濾器是不是愛不釋手呢？詳細的 Filters 可以查看 [API](https://011.vuejs.org/api/filters.html)。

不過到了 Vue 2.x，開發團隊決定將功能移除，轉變為使用者自訂 Filters，

針對團隊的相關討論可以看看：[在 Vue 2.0 中重建被移除的 Filters](http://www.panigale.com.tw/%E5%9C%A8-vue-2-0-%E4%B8%AD%E9%87%8D%E5%BB%BA%E8%A2%AB%E7%A7%BB%E9%99%A4%E7%9A%84-filters/)。

### ［現行使用 - 親手打造］

到了 Vue 2.x，我們則可透過 filters function，自行建立過濾器，

就讓我們偉大的過濾器起死回生吧！

![20160727170557391426.jpg](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-08-02_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB5%EF%BC%BD%E8%B5%B7%E6%AD%BB%E5%9B%9E%E7%94%9F%E9%81%8E%E6%BF%BE%E5%99%A8/20160727170557391426.jpg)

以下的程式碼將打造一個屬於我們自己的過濾器：

別忘了引用回原本 Vue 2.x 版本。

```html
<script src='https://cdnjs.cloudflare.com/ajax/libs/vue/2.4.2/vue.js'></script>
```

撰寫程式碼：

```html
<h1>VueJS - Filter</h1>

<div>
    {{label}} -> {{ label | upper }}
</div>

<script>
    new Vue({
        el: 'div',
        data: {
            label: 'abc'
        },
        filters: {
            upper(value) {
                return value.toUpperCase();
            }
        }
    });
</script>
```

以上我們在建立一個 filter：

```javascript
filters:{

}
```

在裡面自訂了一個 function upper，並且直接 return 一個新的值，

如此一來就完成了一個自訂的過濾器。

### ［現行使用 - 引用套件］

除此之外，想必一定很多人懷念過去的過濾器，

因此也有人寫了基於 Vue 的 filter 套件：[vue2-filters](https://github.com/freearhey/vue2-filters)。

我們只要引用，就可以延續以往的使用方式囉～

從 cdn 引用：

```html
<script src="https://cdn.jsdelivr.net/vue2-filters/0.1.9/vue2-filters.min.js"></script>
```

程式碼的部分就直接以原本 Vue 1.x 的版本去撰寫：

```html
<h1>VueJS - Filter</h1>

<div>
    {{label}} -> {{ label | uppercase  }}
</div>

<script>
    new Vue({
        el: 'div',
        data: {
            label: 'abc'
        },
    });
</script>
```

使用的方法還有很多種，在 [vue2-filters](https://github.com/freearhey/vue2-filters) 開發者的 Github 上都有說明，諸如：

capitalize

```javascript
{{ msg | capitalize }} // 'abc' => 'Abc'
```

uppercase

```javascript
{{ msg | uppercase }} // 'abc' => 'ABC'
```

lowercase

```javascript
{{ msg | lowercase }} // 'ABC' => 'abc'
```

placeholder

```javascript
{{ msg | placeholder('Text if msg is missing') }} // '' => 'Text if msg is missing'
```

truncate

```javascript
{{ msg | truncate(10) }} // 'lorem ipsum dolor' => 'lorem ipsu...'
```

currency

```javascript
{{ amount | currency }} // 12345 => $12,345.00
```

本篇內容較為簡短，希望對於有 filter 需求的朋友能有所幫助！

有勘誤之處，不吝指教。ob'\_'ov