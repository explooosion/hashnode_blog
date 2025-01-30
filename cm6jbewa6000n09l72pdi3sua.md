---
title: "Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［4］為魔法上屬性吧"
seoTitle: "Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［4］為魔法上屬性吧"
seoDescription: "記錄著從 Vue 新手村出發的練功歷程..."
datePublished: Sun Jul 30 2017 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbewa6000n09l72pdi3sua
slug: vuejs-20-vue-4
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/banner/ubiaoqing7c6c595648393ea9928dacf967dd7111.jpg
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/banner/ubiaoqing7c6c595648393ea9928dacf967dd7111.jpg
tags: vue

---

記錄著從 Vue 新手村出發的練功歷程...

本篇任務指引：
-------

1.  學會屬性（Attribute）的綁定

今天想要分享如何針對網頁元件進行一些屬性（Attribute）的新增綁定，

首先，既然是以最最最初心者的角度撰寫本篇，

總得要解釋一下何謂[屬性（Attribute）](https://www.w3schools.com/html/html_attributes.asp)。

根據 [W3S](https://www.w3schools.com/) 說明：

「All HTML elements can have attributes.」

每一個網頁元件都有自己的屬性，

例如 <a></a> 就是超連結，完整的使用：

```html
<a href="https://dotblogs.com.tw/explooosion" target="_blank">帶著 Vue 框架闖蕩異世界</a>
```

上面例子中屬性就有：

*   href：超連結目標網址
*   target：點擊後呈現方式

好！想必各位一定看了快爆炸了，這麼簡單還要提！！！

![ubiaoqing7c6c595648393ea9928dacf967dd7111.jpg](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/ubiaoqing7c6c595648393ea9928dacf967dd7111.jpg)

OK，這麼多的屬性，如果我們不希望他被寫死，

假設有個超連結，尚未設定任何屬性：

```html
<a>帶著 Vue 框架闖蕩異世界</a>
```

透過設定的方式，通常有以下方法：

**［JavaScript］**

```javascript
document.getElementsByTagName('a')[0].setAttribute('href','https://dotblogs.com.tw/explooosion');
```

**［JQuery］**

```javascript
$('a').attr('href','https://dotblogs.com.tw/explooosion');
```

那麼在 Vue 中要如何使用呢？

首先對準地面釋放魔力：

![Characters-39445.gif](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/Characters-39445.gif)

畫陣後就可以練成惹：

![1324282879-531464755.gif](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/1324282879-531464755.gif)

．．．

### ［基本設定］

在 Vue 中，我們會使用到「v-bind」，指定我們要的值，

參照上述的範例我們實際寫寫看：

```html
<h1>VueJS - Bind</h1>

<a v-bind:href="url">帶著 Vue 框架闖蕩異世界</a>

<script>
    new Vue({
        el: 'a',
        data: {
            url: 'https://dotblogs.com.tw/explooosion'
        }
    });
</script>
```

利用 vind: 後面接著我們要設定的屬性，就可以進行屬性的綁定，

至於 url 就是變數，我們在 data：｛｝ 裡面進行宣告，

設定為字串：https://dotblogs.com.tw/explooosion，

如此一來就可進行屬性的設定。

是不是很簡單呢～！

![gj1309149158652825974546.gif](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/gj1309149158652825974546.gif)

### ［多種設定方法］

在屬性綁定上其實有很多種作法都可達到，Vue 提供了以下三種：

1.  ##### v-bind:href="url"
    
2.  ##### v-bind="{ href : url }"
    
3.  ##### :href="url"
    

在使用上結果並不會有差異，其實第三種算是提供簡寫的方法，

而我們可以依據需求或喜好進行設定，正所謂殊途同歸。

```html
<a v-bind:href="url">VueJS</a>
<a :href="url">VueJS</a>
<a v-bind="{ href : url }">VueJS</a>
```

### ［條件式設定］

說明之前我們先實作透過 v-bind 的方式設定 class：

```html
<style>
    .selected {
        color: #f00;
    }
</style>
```
```html
<h1>VueJS - Bind</h1>

<span :class="isSelected">帶著 Vue 框架闖蕩異世界</span>

<script>
    new Vue({
        el: 'span',
        data: {
            isSelected: 'selected',
        }
    });
</script>
```

*   在 data 中的 isSelected 是一個變數，其值為字串 'selected'

實際畫面：

![1501418381_0729.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/1501418381_0729.png)

上述我們利用 :class 方式設定，透過 chrome debug （F12）觀察：

[![1501418351_96597.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/1501418351_96597.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/bb943e18-4e7a-49a8-a9f3-29d5e15085a8/1501418351_96597.png)

*   其實就是 class="selected"

接下來提到的是透過條件的判斷，決定是否使用該 class，

當條件成立時（true）才會進行設定：

```html
<h1>VueJS - Bind</h1>

<span :class="{ selected : isSelected }">帶著 Vue 框架闖蕩異世界</span>

<script>
    new Vue({
        el: 'span',
        data: {
            isSelected: true
        }
    });
</script>
```

此時，data 中的變數 isSelected 是一個布林值（bool），

如果設定 true，那麼該條件式 { selected : isSelected } 就會成立。

實際畫面：

... 跟剛剛上述一樣就不貼了~

如果改成 false：

![1501419214_19211.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/1501419214_19211.png)

### ［動腦探討］

值得一提的是，因為條件不成立那麼檢視結果會是什麼呢？

第一種結果：

```html
<span>帶著 Vue 框架闖蕩異世界</span>
```

第二種結果：

```html
<span class="false">帶著 Vue 框架闖蕩異世界</span>
```

第三種結果：

```html
<span class="">帶著 Vue 框架闖蕩異世界</span>
```

第四種結果：

```html
<span class>帶著 Vue 框架闖蕩異世界</span>
```

神明來電告訴你答案：

![RmmBhaMPiwHEPR5L.gif!webindex](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/RmmBhaMPiwHEPR5L.gif!webindex)

神明：「F12 給他開下去看看！！」

[![1501419524_27855.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/1501419524_27855.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/bb943e18-4e7a-49a8-a9f3-29d5e15085a8/1501419524_27855.png)

你答對了嗎？？？

其實我也猜錯，我還以為是空的第三種。

### ［三元式設定］

如果我們希望利用三元式運算來表達，就要把大括號 { } 改為中括號 \[ \] ，

當 isSelected 為 true 的時候，就會帶入 'selected ' 字串，否則為空的。

```html
<span :class="[ isSelected ? 'selected' : '' ]">帶著 Vue 框架闖蕩異世界</span>
```

你也可以把該字串改成利用讀取 data 中的變數：

```html
<span :class="[ isSelected ? className : '' ]">帶著 Vue 框架闖蕩異世界</span>
```

然後到 Vue 的 data 中新增一個變數 className：

```javascript
new Vue({
    el: 'span',
    data: {
        isSelected: true,
        className: 'selected'
    }
});
```

實際畫面會是一樣的：

![1501418381_0729.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/1501418381_0729.png)

如果當條件為否的時候，把原本的空字串改為別的 class 名稱，

同樣就可以套用該 class。

如法炮製，我們額外新增一個 class「unselected」：

```html
<style>
    .selected {
        color: red;
    }

    .unselected {
        color: #0f0;
    }
</style>
```
```html
<h1>VueJS - Bind</h1>
　
<span :class="[ isSelected ? 'selected' : 'unselected' ]">帶著 Vue 框架闖蕩異世界</span>
<script>
    new Vue({
        el: 'span',
        data: {
            isSelected: false
        }
    });
</script>
```

當 false 的時候 class 就會套用 unselected，也就變成綠色了！

![1501421303_85984.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/1501421303_85984.png)

### ［以陣列形式設定］

為什麼要使用陣列呢？

當如果我們 class 不只想套用一個的時候，就會使用到～

假如我們有這麼多的樣式：

```css
.font-size {
    font-size: 1.5em;
}

.font-color {
    color: #f0f;
}

.font-weight {
    font-weight: bold;
}

.font-underline {
    text-decoration: underline;
}
```

利用陣列的方式就可套用，同時也能夠混搭三元式判斷：

```html
<h1>VueJS - Bind</h1>

<span :class="[ 'font-size','font-color','font-weight', hasLine ? 'font-underline' : '' ]">帶著 Vue 框架闖蕩異世界</span>
<script>
    new Vue({
        el: 'span',
        data: {
            hasLine: true
        }
    });
</script>
```

畫面結果：

[![1501421979_96165.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/1501421979_96165.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/bb943e18-4e7a-49a8-a9f3-29d5e15085a8/1501421979_96165.png)

對於混搭的條件式更好的寫法：

```html
<span :class="[ 'font-size','font-color','font-weight', { 'font-underline' : hasLine } ]">帶著 Vue 框架闖蕩異世界</span>
```

*   直接利用 {  } 就可做到，不過這是沒有「否則」的條件哦～

### ［其他屬性］

最後補充一下～～

除了以上提到的 class ，我們也可以設定很多其他屬性。

例如 id：

```html
<h1>VueJS - Bind</h1>

<span :id="idValue">帶著 Vue 框架闖蕩異世界</span>
<script>
    new Vue({
        el: 'span',
        data: {
            idValue: "span1"
        }
    });
</script>
```

畫面結果：

[![1501422971_20764.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/1501422971_20764.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/bb943e18-4e7a-49a8-a9f3-29d5e15085a8/1501422971_20764.png)

  
以上為針對 v-bind 的筆記分享，希望對各位有幫助。

趕快慶祝一下吧！～

![giphy.gif](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-30_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB4%EF%BC%BD%E7%82%BA%E9%AD%94%E6%B3%95%E4%B8%8A%E5%B1%AC%E6%80%A7%E5%90%A7/giphy.gif)

### Next Stop：

### [Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［5］起死回生過濾器](https://dotblogs.com.tw/explooosion/2017/08/02/183659)

有勘誤之處，不吝指教。ob'\_'ov